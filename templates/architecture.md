# Introduction

## Purpose

This document describes the architecture of the Real-Time Analytics Platform (RTAP), a system that ingests, processes, and visualizes streaming data from IoT sensors deployed across manufacturing facilities. It serves as the authoritative reference for system design decisions, component interactions, and deployment topology.

## Scope

This architecture covers:

- Data ingestion from edge devices and sensors
- Stream processing and real-time aggregation
- Storage layer for time-series and dimensional data
- Visualization and alerting subsystems
- Security and access control

## Architecture Principles

| Principle | Description |
|---|---|
| Event-driven | All inter-service communication uses asynchronous events |
| Horizontally scalable | Each component scales independently based on load |
| Fault-tolerant | No single point of failure; graceful degradation |
| Observable | Every component emits metrics, logs, and traces |
| Secure by default | Zero-trust networking, encryption everywhere |

# System Architecture

## High-Level Overview

The platform follows a layered architecture with clear separation between ingestion, processing, storage, and presentation:

```
┌─────────────────────────────────────────────────────────┐
│                    Presentation Layer                     │
│   Dashboard App  │  Alert Manager  │  API Gateway        │
├─────────────────────────────────────────────────────────┤
│                    Processing Layer                       │
│   Stream Processor (Flink)  │  Batch Aggregator (Spark)  │
├─────────────────────────────────────────────────────────┤
│                    Storage Layer                          │
│   TimescaleDB  │  Redis Cache  │  S3 (Data Lake)        │
├─────────────────────────────────────────────────────────┤
│                    Ingestion Layer                        │
│   MQTT Broker  │  Kafka  │  Schema Registry              │
├─────────────────────────────────────────────────────────┤
│                    Edge Layer                             │
│   IoT Gateway  │  Edge Compute  │  Sensor Firmware       │
└─────────────────────────────────────────────────────────┘
```

## Component Details

### Ingestion Layer

| Component | Technology | Purpose | Throughput |
|---|---|---|---|
| MQTT Broker | EMQX 5.x | Sensor data ingestion | 100K msg/s |
| Message Bus | Apache Kafka 3.6 | Event streaming backbone | 500K msg/s |
| Schema Registry | Confluent | Schema evolution, validation | — |
| Edge Gateway | Custom (Rust) | Protocol translation, buffering | 50K msg/s per node |

### Processing Layer

The stream processor consumes from Kafka, applies windowed aggregations (tumbling and sliding windows), enriches events with dimensional data, and writes results to both the cache and the time-series database.

Key processing pipelines:

1. **Sensor Aggregation** — 1-minute tumbling windows, computes min/max/avg/p99 per sensor
2. **Anomaly Detection** — Sliding window (5 min), z-score based, triggers alerts
3. **Equipment Health** — Session windows per machine, computes uptime and degradation metrics

### Storage Layer

| Store | Technology | Use Case | Retention |
|---|---|---|---|
| Time-series | TimescaleDB | Sensor readings, aggregates | 90 days hot, 2 years cold |
| Cache | Redis Cluster | Real-time dashboards, last-known values | TTL-based |
| Data Lake | S3 + Parquet | Historical analysis, ML training | Indefinite |
| Metadata | PostgreSQL | Device registry, user configs | Indefinite |

# Deployment Architecture

## Infrastructure

The platform runs on AWS across two regions (us-east-1 primary, us-west-2 DR) using EKS for container orchestration.

| Resource | Specification | Count |
|---|---|---|
| EKS Node Group (compute) | m6i.2xlarge | 8–24 (auto-scaling) |
| EKS Node Group (Kafka) | r6i.2xlarge | 6 (fixed) |
| TimescaleDB | db.r6g.2xlarge | 3-node HA |
| Redis Cluster | cache.r6g.xlarge | 6 nodes (3 primary + 3 replica) |
| S3 | Standard + Glacier | — |

## Disaster Recovery

- **RPO**: < 1 minute (Kafka cross-region replication)
- **RTO**: < 15 minutes (automated failover via Route 53)
- **Backup**: Daily TimescaleDB snapshots, continuous Kafka mirroring
- **Runbook**: Automated DR drill executed monthly

> [!note]
> Cross-region Kafka mirroring uses MirrorMaker 2. Topic configurations, consumer offsets, and ACLs are automatically replicated.

# Security Architecture

## Network Security

- All inter-service traffic encrypted with mTLS (Istio service mesh)
- Network policies enforce least-privilege pod-to-pod communication
- External access only through API Gateway (Kong) with rate limiting
- WAF (AWS WAF) protects public endpoints

## Data Security

| Data Classification | Encryption at Rest | Encryption in Transit | Access Control |
|---|---|---|---|
| Sensor readings | AES-256 (S3 SSE) | TLS 1.3 | Role-based |
| User credentials | AES-256 + KMS | TLS 1.3 | Privileged access only |
| API keys | AES-256 + KMS | TLS 1.3 | Service accounts |
| Audit logs | AES-256 (WORM) | TLS 1.3 | Security team only |
