# Introduction

## Purpose

This Data Protection Impact Assessment (DPIA) is conducted in accordance with Article 35 of the General Data Protection Regulation (EU) 2016/679. It evaluates the necessity, proportionality, and risks of the proposed data processing activity and identifies measures to mitigate those risks.

## Processing Activity Under Assessment

| Field | Detail |
|---|---|
| Activity Name | Customer Behavioral Analytics Platform |
| Data Controller | Nexus Solutions GmbH |
| DPO Contact | dpo@nexus-solutions.eu |
| Assessment Date | June 25, 2026 |
| Review Date | June 25, 2027 |
| Status | Draft / Under Review / Approved |

## Legal Basis for DPIA

This DPIA is required because the processing activity involves:

- [x] Systematic and extensive profiling with significant effects (Art. 35(3)(a))
- [ ] Large-scale processing of special category data (Art. 35(3)(b))
- [x] Systematic monitoring of a publicly accessible area (Art. 35(3)(c))
- [x] Processing listed on the supervisory authority's mandatory DPIA list

# Description of Processing

## Nature of Processing

The Customer Behavioral Analytics Platform collects and analyzes user interaction data across the Nexus product suite to generate behavioral profiles, predict churn risk, and personalize the user experience. Processing includes:

1. **Collection** — User clickstream data, feature usage metrics, session recordings, and support interaction logs
2. **Aggregation** — Raw events consolidated into per-user behavioral profiles updated hourly
3. **Analysis** — Machine learning models score each user on engagement, churn risk, and upsell propensity
4. **Action** — Scores trigger automated workflows (in-app messages, email campaigns, CSM alerts)

## Scope of Processing

| Dimension | Detail |
|---|---|
| Data subjects | ~45,000 active end users across 1,200 customer organizations |
| Geographic scope | EU/EEA (primary), UK, Switzerland |
| Data volume | ~12M events/day, ~500GB/month |
| Retention period | Raw events: 90 days · Aggregated profiles: 2 years · ML model outputs: 1 year |
| Recipients | Internal teams (Product, CS, Marketing) · Sub-processors (see Section 6) |

## Categories of Personal Data

| Category | Examples | Special Category? |
|---|---|---|
| Identifiers | User ID, email, IP address, device fingerprint | No |
| Usage data | Pages visited, features used, time on page, click paths | No |
| Session recordings | Mouse movements, scroll depth, form interactions | No |
| Communication data | Support ticket content, chat transcripts | No |
| Derived data | Engagement score, churn probability, user segment | No |

> [!important]
> No special category data (Art. 9) is intentionally collected. Session recordings are configured to mask all free-text input fields to prevent inadvertent capture of sensitive data.

## Purpose of Processing

| Purpose | Legal Basis (Art. 6) | Description |
|---|---|---|
| Product improvement | Legitimate interest (Art. 6(1)(f)) | Aggregate analytics to improve UX and feature prioritization |
| Churn prediction | Legitimate interest (Art. 6(1)(f)) | Identify at-risk accounts for proactive customer success |
| Personalization | Consent (Art. 6(1)(a)) | Personalized in-app guidance and recommendations |
| Marketing segmentation | Consent (Art. 6(1)(a)) | Targeted email campaigns based on usage patterns |

# Necessity and Proportionality

## Necessity Assessment

| Question | Assessment |
|---|---|
| Is the processing necessary for the stated purpose? | Yes — aggregate metrics alone are insufficient for individual churn prediction |
| Could the purpose be achieved with less data? | Partially — session recordings could be replaced with structured event data (see mitigation M-03) |
| Could the purpose be achieved without personal data? | No — individual-level analysis is required for personalization and churn prediction |
| Is the retention period justified? | 2-year profile retention aligns with typical customer lifecycle; raw data is deleted after 90 days |

## Proportionality Assessment

The processing is proportionate because:

1. **Data minimization** — Only product interaction data is collected; no external data enrichment
2. **Purpose limitation** — Data is used only for product improvement, customer success, and consented marketing
3. **Storage limitation** — Tiered retention with automatic deletion (90 days raw, 2 years aggregated)
4. **Transparency** — Users are informed via privacy notice and cookie consent banner with granular controls

# Risk Assessment

## Identified Risks

| ID | Risk | Likelihood | Severity | Overall Risk |
|---|---|---|---|---|
| R-01 | Unauthorized access to behavioral profiles | Low | High | Medium |
| R-02 | Re-identification from aggregated data | Low | Medium | Low |
| R-03 | Session recordings capture sensitive input | Medium | High | High |
| R-04 | Profiling leads to discriminatory outcomes | Low | High | Medium |
| R-05 | Data breach during cross-border transfer | Low | Critical | Medium |
| R-06 | Excessive retention beyond stated periods | Medium | Medium | Medium |
| R-07 | Insufficient consent mechanism for personalization | Medium | High | High |
| R-08 | Sub-processor non-compliance | Low | High | Medium |

## Risk Matrix

| | Low Severity | Medium Severity | High Severity | Critical Severity |
|---|---|---|---|---|
| **High Likelihood** | Medium | High | Very High | Very High |
| **Medium Likelihood** | Low | Medium | **High (R-03, R-07)** | High |
| **Low Likelihood** | Low | **Low (R-02)** | **Medium (R-01, R-04, R-08)** | **Medium (R-05)** |

# Mitigation Measures

| ID | Risk | Measure | Responsible | Deadline | Status |
|---|---|---|---|---|---|
| M-01 | R-01 | Implement role-based access control with quarterly review | Security Team | Q3 2026 | In Progress |
| M-02 | R-02 | Apply k-anonymity (k≥5) to all exported aggregate reports | Data Engineering | Q3 2026 | Not Started |
| M-03 | R-03 | Replace full session recordings with structured event capture; mask all input fields | Product Team | Q3 2026 | In Progress |
| M-04 | R-04 | Conduct bias audit on ML models quarterly; document in fairness report | ML Team | Ongoing | Active |
| M-05 | R-05 | Implement Standard Contractual Clauses (SCCs) for all cross-border transfers | Legal | Complete | Done |
| M-06 | R-06 | Automate data deletion via lifecycle policies with monthly compliance check | Data Engineering | Q3 2026 | In Progress |
| M-07 | R-07 | Redesign consent banner with granular purpose selection; implement consent withdrawal API | Product Team | Q3 2026 | Not Started |
| M-08 | R-08 | Annual sub-processor audit program; add termination clause for non-compliance | Legal / Procurement | Q4 2026 | Not Started |

# Sub-Processors

| Sub-processor | Purpose | Location | Transfer Mechanism | Last Audit |
|---|---|---|---|---|
| AWS (Frankfurt) | Infrastructure hosting | EU (Frankfurt) | N/A (EU-based) | March 2026 |
| Snowflake | Data warehousing | EU (Amsterdam) | N/A (EU-based) | January 2026 |
| Mixpanel | Event analytics | US | SCCs + supplementary measures | February 2026 |
| Intercom | In-app messaging | US | SCCs + supplementary measures | April 2026 |

> [!warning]
> Mixpanel and Intercom process data in the United States. Standard Contractual Clauses (Module 2: Controller to Processor) are in place, supplemented by encryption in transit and at rest, and contractual commitments to challenge government access requests.

# Data Subject Rights

| Right | Implementation | Response Time |
|---|---|---|
| Access (Art. 15) | Automated export via privacy dashboard | < 72 hours |
| Rectification (Art. 16) | Self-service profile editing | Immediate |
| Erasure (Art. 17) | Automated deletion pipeline triggered via dashboard or support | < 30 days |
| Restriction (Art. 18) | Processing flag in user record; excludes from ML pipelines | < 72 hours |
| Data portability (Art. 20) | JSON export of all personal data | < 72 hours |
| Object to profiling (Art. 21) | Opt-out toggle in privacy settings; disables all ML scoring | Immediate |

# Consultation

## Internal Consultation

| Stakeholder | Date | Outcome |
|---|---|---|
| Data Protection Officer | June 10, 2026 | Approved with conditions (M-03, M-07 required before launch) |
| Information Security | June 12, 2026 | Approved; recommended M-01 priority elevation |
| Legal Counsel | June 15, 2026 | Approved; SCCs reviewed and updated |
| Works Council | June 18, 2026 | No objections raised |

## Supervisory Authority Consultation

Prior consultation with the supervisory authority (Art. 36) is **not required** because the residual risk after mitigation measures is reduced to an acceptable level. This determination will be reviewed if:

- Mitigation measures M-03 or M-07 are not implemented by Q3 2026
- The scope of processing expands to include special category data
- A data breach occurs involving the analytics platform

# Approval

| Role | Name | Date | Decision |
|---|---|---|---|
| Data Protection Officer | Dr. Lisa Hofmann | | |
| Head of Product | Marcus Weber | | |
| CISO | Anna Bergström | | |
| Managing Director | Thomas Richter | | |

> [!note]
> This DPIA must be reviewed annually or when there is a significant change to the processing activity, whichever comes first. The next scheduled review is June 2027.
