# System and Organization Controls (SOC 2) Type II Report

## Scope and Objectives

### System Description

Acme Cloud Platform ("the System") provides enterprise customers with a managed infrastructure-as-a-service (IaaS) solution, including compute, storage, networking, and identity management services. The System is hosted across three AWS regions (us-east-1, us-west-2, eu-west-1) and serves approximately 2,400 enterprise customers.

This report covers the period from January 1, 2026 through June 30, 2026.

### Trust Services Criteria

This examination was conducted in accordance with the AICPA Trust Services Criteria for:

| Category | Criteria | Applicable |
|---|---|---|
| Security | CC1.0 – CC9.0 | Yes |
| Availability | A1.1 – A1.3 | Yes |
| Processing Integrity | PI1.1 – PI1.5 | Yes |
| Confidentiality | C1.1 – C1.2 | Yes |
| Privacy | P1.0 – P8.0 | No |

### Boundaries of the System

The system boundaries include:

- **Infrastructure**: AWS VPCs, EC2 instances, S3 buckets, RDS databases, and CloudFront distributions
- **Software**: Acme Platform v4.x application stack, API gateway, monitoring agents
- **People**: Engineering (42 FTE), SRE (8 FTE), Security (6 FTE), Compliance (3 FTE)
- **Data**: Customer configuration data, usage metrics, access logs, billing records

> [!important]
> Customer-uploaded data processed by the platform is explicitly excluded from the scope of this report. Acme acts as a data processor; the customer retains ownership and responsibility for their data.

## Control Environment

### Governance Structure

The Board of Directors maintains oversight of the control environment through the Audit Committee, which meets quarterly. Management has established the following governance bodies:

1. **Security Steering Committee** — meets monthly; reviews security posture, incident trends, and policy exceptions
2. **Change Advisory Board (CAB)** — meets weekly; reviews and approves production changes
3. **Risk Management Committee** — meets quarterly; maintains the enterprise risk register

### Risk Assessment Process

Acme performs a formal risk assessment annually, with continuous monitoring of risk indicators throughout the year. The methodology follows ISO 31000:2018 and considers:

- Likelihood (1–5 scale)
- Impact (1–5 scale, across financial, operational, reputational, and compliance dimensions)
- Inherent vs. residual risk after controls

The current risk register contains 47 identified risks, of which 3 are rated "High" residual risk and are tracked with mitigation plans reviewed monthly.

## Logical and Physical Access Controls

### Authentication

All access to production systems requires multi-factor authentication (MFA). The following authentication mechanisms are enforced:

| System | Method | MFA Required | Session Timeout |
|---|---|---|---|
| AWS Console | SSO via Okta | Yes (TOTP/WebAuthn) | 1 hour |
| Production SSH | Certificate-based | Yes (hardware key) | 30 minutes |
| API Gateway | OAuth 2.0 + mTLS | N/A (certificate) | Token-based |
| Admin Dashboard | SAML 2.0 via Okta | Yes (push notification) | 4 hours |
| Database (RDS) | IAM authentication | Yes (inherited) | Connection-based |

### Access Reviews

Quarterly access reviews are performed for all production systems. The review process includes:

1. **Automated extraction** of current access grants from IAM, Okta, and database privilege tables
2. **Manager certification** — each manager reviews and certifies access for their direct reports
3. **Privileged access review** — Security team reviews all administrative and elevated access
4. **Remediation** — unauthorized or excessive access is revoked within 24 hours of identification

During the audit period, 100% of scheduled access reviews were completed on time. 12 access revocations were identified and remediated, with an average remediation time of 4.2 hours.

## Change Management

### Change Control Process

All changes to production systems follow a documented change control process:

```
Developer → Code Review (2 approvers) → Automated Tests → Staging Deploy
→ QA Validation → CAB Approval (for significant changes) → Production Deploy
→ Post-deploy monitoring (30 min)
```

### Change Categories

| Category | Approval Required | Examples |
|---|---|---|
| Standard | Pre-approved, automated | Dependency patches, config flag toggles |
| Normal | Peer review + team lead | Feature releases, API changes, schema migrations |
| Significant | CAB approval | Infrastructure changes, security control modifications |
| Emergency | Post-hoc CAB review | Critical security patches, incident remediation |

During the audit period:
- **1,247** total changes deployed to production
- **98.3%** passed automated testing gates on first attempt
- **0** unauthorized changes detected
- **3** emergency changes executed (all with post-hoc CAB review completed within 48 hours)

## Incident Management

### Incident Classification

| Severity | Definition | Response SLA | Resolution SLA |
|---|---|---|---|
| P1 — Critical | Service outage affecting >50% of customers | 15 minutes | 4 hours |
| P2 — Major | Degraded performance or partial outage | 30 minutes | 8 hours |
| P3 — Minor | Isolated issue, workaround available | 2 hours | 48 hours |
| P4 — Low | Cosmetic or non-impacting issue | 8 hours | 5 business days |

### Incident Summary

During the audit period, the following incidents were recorded:

- **P1 incidents**: 1 (database failover event on March 14, 2026; resolved in 2h 47m)
- **P2 incidents**: 4 (average resolution time: 5h 12m)
- **P3 incidents**: 23
- **P4 incidents**: 89

All P1 and P2 incidents had root cause analyses completed and published within 5 business days, with preventive measures tracked to completion.

## Monitoring and Logging

### Log Collection

All production systems forward logs to a centralized SIEM (Splunk Enterprise) with the following retention policies:

| Log Type | Retention | Encryption | Tamper Protection |
|---|---|---|---|
| Authentication logs | 2 years | AES-256 at rest | Write-once storage |
| API access logs | 1 year | AES-256 at rest | Immutable bucket |
| System/application logs | 90 days | AES-256 at rest | Standard |
| Network flow logs | 90 days | AES-256 at rest | Standard |
| Database audit logs | 2 years | AES-256 at rest | Write-once storage |

> [!note]
> All log data is encrypted in transit using TLS 1.3 and at rest using AES-256. Authentication and database audit logs are stored in write-once (WORM) storage to prevent tampering.

## Conclusion

Based on the examination of the controls described above, the service auditor's opinion is that Acme Cloud Platform's controls were suitably designed and operating effectively throughout the period January 1, 2026 through June 30, 2026, to meet the applicable trust services criteria for Security, Availability, Processing Integrity, and Confidentiality.
