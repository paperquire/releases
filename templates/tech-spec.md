# Scope

## Purpose

This document defines the technical specification for the Customer Data Integration (CDI) interface between the Billing Management System (BMS) and the Enterprise Data Warehouse (EDW). It covers message formats, protocols, error handling, and operational requirements.

## Audience

This specification is intended for:

- Integration architects and developers responsible for implementing the interface
- Operations teams managing the production data pipeline
- Quality assurance teams validating data integrity

## References

| Document | Version | Description |
|---|---|---|
| CDI Architecture Overview | 2.1 | High-level integration architecture |
| BMS API Guide | 4.0 | Billing system REST API reference |
| EDW Data Model | 3.2 | Warehouse schema and entity definitions |
| Security Standards | 1.5 | Enterprise encryption and auth requirements |

# Interface Overview

## Data Flow

The CDI interface transmits customer account records from BMS to EDW on a near-real-time basis. Records are published as events to an Apache Kafka topic, consumed by the EDW ingestion service, transformed, and loaded into staging tables.

```
BMS → Kafka Topic (cdi.customer.events) → EDW Ingestion Service → Staging → Production Tables
```

## Message Format

All messages use JSON encoding with the following envelope:

```json
{
  "messageId": "uuid-v4",
  "timestamp": "2026-06-25T14:30:00Z",
  "source": "BMS",
  "eventType": "CUSTOMER_UPDATE",
  "version": "2.0",
  "payload": { }
}
```

### Event Types

| Event Type | Trigger | Payload Schema |
|---|---|---|
| CUSTOMER_CREATE | New account provisioned | `customer-create-v2.json` |
| CUSTOMER_UPDATE | Account field modified | `customer-update-v2.json` |
| CUSTOMER_DEACTIVATE | Account closed | `customer-deactivate-v1.json` |
| ADDRESS_CHANGE | Service address updated | `address-change-v2.json` |

# Technical Requirements

## Protocol Specifications

### Kafka Configuration

| Parameter | Value | Notes |
|---|---|---|
| Bootstrap Servers | `kafka-prod-01:9092,kafka-prod-02:9092` | Production cluster |
| Topic | `cdi.customer.events` | Partitioned by account ID |
| Partitions | 12 | Scaled for throughput |
| Replication Factor | 3 | Across availability zones |
| Retention | 7 days | Per compliance policy |
| Compression | LZ4 | Optimized for throughput |
| Security Protocol | SASL_SSL | mTLS + SCRAM-SHA-256 |

### Message Guarantees

- **Delivery**: At-least-once (consumer handles idempotency via `messageId`)
- **Ordering**: Per-partition ordering guaranteed (messages keyed by `accountId`)
- **Max message size**: 1 MB (compressed)
- **Throughput target**: 5,000 messages/second sustained, 15,000 burst

## Authentication and Authorization

All Kafka clients authenticate using mutual TLS with SCRAM-SHA-256. Certificates are issued by the enterprise PKI and rotated every 90 days.

> [!important]
> Service accounts must be provisioned through the Identity Access Management (IAM) portal. Direct certificate issuance is prohibited.

### Required Permissions

| Principal | Topic | Permission |
|---|---|---|
| `svc-bms-producer` | `cdi.customer.events` | WRITE, DESCRIBE |
| `svc-edw-consumer` | `cdi.customer.events` | READ, DESCRIBE |
| `svc-monitoring` | `cdi.customer.events` | DESCRIBE |

## Error Handling

### Retry Policy

Failed message deliveries are retried with exponential backoff:

1. **Attempt 1**: Immediate retry
2. **Attempt 2**: 1 second delay
3. **Attempt 3**: 5 second delay
4. **Attempt 4**: 30 second delay
5. **Dead Letter Queue**: After 4 failed attempts, message is routed to `cdi.customer.events.dlq`

### Dead Letter Queue Processing

Messages in the DLQ are:
- Retained for 30 days
- Monitored via PagerDuty alert (P3 severity)
- Manually reviewed and replayed by the integration support team

## Data Validation

### Required Field Validation

All inbound messages are validated against JSON Schema before processing. The following fields are mandatory:

| Field | Type | Constraint |
|---|---|---|
| `accountId` | string | UUID v4 format |
| `timestamp` | string | ISO 8601 with timezone |
| `eventType` | string | Enum: CREATE, UPDATE, DEACTIVATE |
| `payload.firstName` | string | 1–100 characters |
| `payload.lastName` | string | 1–100 characters |
| `payload.email` | string | RFC 5322 compliant |

### Transformation Rules

The EDW ingestion service applies the following transformations:

1. **Deduplication** — Messages with duplicate `messageId` within a 24-hour window are dropped
2. **Enrichment** — Geographic coordinates appended via address geocoding service
3. **Normalization** — Phone numbers converted to E.164 format
4. **Masking** — SSN and financial fields masked before loading to non-restricted schemas

# Operational Requirements

## Monitoring

| Metric | Threshold | Alert |
|---|---|---|
| Consumer lag | > 10,000 messages | P2 — PagerDuty |
| Message processing errors | > 1% of volume | P3 — PagerDuty |
| DLQ depth | > 100 messages | P3 — Slack |
| End-to-end latency (p99) | > 30 seconds | P3 — Dashboard |
| Producer availability | < 99.9% | P1 — PagerDuty |

## SLA Targets

- **Availability**: 99.95% uptime (measured monthly)
- **Latency**: 95th percentile end-to-end < 5 seconds
- **Data freshness**: EDW reflects BMS changes within 60 seconds under normal load
- **Recovery Time Objective (RTO)**: 15 minutes
- **Recovery Point Objective (RPO)**: 0 messages (no data loss)
