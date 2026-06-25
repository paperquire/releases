# Document Information

## Assessment Details

| Field | Detail |
|---|---|
| AI System Name | PredictFlow — Automated Credit Scoring Engine |
| Provider | FinTech Analytics SE |
| Version | 2.4.1 |
| Assessment Date | June 25, 2026 |
| Assessor | Internal Conformity Assessment Body (Art. 43(1)) |
| Risk Classification | High-Risk (Annex III, Section 5(b) — creditworthiness assessment) |
| Applicable Regulation | Regulation (EU) 2024/1689 (EU AI Act) |
| Status | Compliant with conditions |

## System Description

PredictFlow is an AI-powered credit scoring engine that assesses the creditworthiness of individuals applying for consumer credit products. The system processes applicant financial data, employment history, and publicly available credit registry information to generate a credit score (0–1000) and a binary lending recommendation (approve/decline).

> [!important]
> As a high-risk AI system under Annex III, Section 5(b), PredictFlow is subject to the full conformity assessment requirements of Chapter 3 (Articles 8–15) of the EU AI Act.

# Risk Classification

## Classification Rationale

| Criterion | Assessment |
|---|---|
| Annex III Category | 5. Access to essential private/public services — (b) creditworthiness evaluation |
| Intended Purpose | Automated assessment of natural persons' creditworthiness |
| Autonomy Level | Decision-support (human reviewer required for decline decisions > €5,000) |
| Scale | ~120,000 assessments/month across 14 EU member states |
| Affected Persons | Natural persons applying for consumer credit |

## Exemption Analysis

| Exemption (Art. 6(3)) | Applicable? | Reasoning |
|---|---|---|
| Narrow procedural task | No | System performs substantive creditworthiness evaluation |
| Intended to improve prior human assessment | Partially | System augments but significantly influences lending decisions |
| Preparatory to a human-reviewed assessment | Yes (for >€5K) | Decline decisions above threshold require human review |
| Detect patterns without replacing human judgment | No | System generates binding scores for auto-approvals |

**Conclusion**: No exemption applies. Full high-risk requirements must be met.

# Risk Management System (Article 9)

## Risk Management Process

The risk management system is a continuous, iterative process maintained throughout the AI system's lifecycle:

| Phase | Activities | Frequency |
|---|---|---|
| Identification | Threat modeling, bias risk identification, adversarial scenario analysis | Quarterly |
| Analysis | Quantitative risk scoring (likelihood × impact), root cause analysis | Quarterly |
| Evaluation | Comparison against risk appetite thresholds, regulatory benchmarks | Quarterly |
| Treatment | Control implementation, model retraining, threshold adjustment | As needed |
| Monitoring | Automated drift detection, performance dashboards, incident tracking | Continuous |

## Identified Risks and Mitigations

| ID | Risk | Category | Likelihood | Impact | Residual Risk | Mitigation |
|---|---|---|---|---|---|---|
| R-01 | Discriminatory bias against protected groups | Fundamental rights | Medium | Critical | Medium | Bias testing across 12 demographic dimensions; fairness constraints in training |
| R-02 | Model performance degradation over time | Accuracy | High | High | Low | Automated drift detection with ±2% accuracy threshold; monthly retraining |
| R-03 | Adversarial input manipulation | Security | Low | High | Low | Input validation, anomaly detection, rate limiting |
| R-04 | Incorrect score due to stale data | Accuracy | Medium | Medium | Low | Real-time data freshness checks; maximum data age of 30 days |
| R-05 | Over-reliance by human reviewers | Human oversight | Medium | High | Medium | Mandatory justification field; random audit of human override decisions |
| R-06 | Privacy violation through data inference | Fundamental rights | Low | High | Low | Feature attribution analysis; prohibited proxy variable detection |

> [!warning]
> Risk R-01 (discriminatory bias) remains at Medium residual risk. While fairness constraints are applied during training, ongoing monitoring has identified a 3.2% approval rate differential for applicants aged 18–25. A targeted retraining initiative is underway with a completion target of Q3 2026.

# Data and Data Governance (Article 10)

## Training Data

| Property | Detail |
|---|---|
| Dataset Name | CreditScore-EU-v4 |
| Size | 8.2M labeled records (2018–2025) |
| Sources | Partner banks (anonymized), public credit registries, Eurostat demographics |
| Geographic coverage | 14 EU member states |
| Label definition | Binary outcome (default/no-default within 24 months) |
| Class balance | 7.8% positive (default), 92.2% negative |

## Data Quality Measures

| Measure | Implementation |
|---|---|
| Completeness checks | Automated pipeline rejects records with >5% missing features |
| Accuracy validation | Cross-referenced against official credit registry records quarterly |
| Bias audit | Demographic parity, equalized odds, and calibration tested across age, gender, nationality |
| Representativeness | Dataset composition compared against Eurostat population statistics; stratified sampling applied |
| Data freshness | Training data refreshed quarterly; model retrained on rolling 5-year window |

## Prohibited Data Practices

The following data categories are explicitly excluded from model inputs per Article 10(5):

- Racial or ethnic origin
- Political opinions
- Religious or philosophical beliefs
- Trade union membership
- Genetic or biometric data
- Health data
- Sexual orientation
- Gender (used only in post-hoc bias audit, never as model input)

# Technical Documentation (Article 11)

## System Architecture

| Component | Technology | Purpose |
|---|---|---|
| Feature Store | Feast on PostgreSQL | Centralized feature management with versioning |
| Model Training | Python 3.11, XGBoost 2.0, Fairlearn | Gradient boosted model with fairness constraints |
| Serving | FastAPI on Kubernetes | Real-time inference API (p99 < 200ms) |
| Monitoring | Evidently AI | Data drift, prediction drift, fairness metrics |
| Explainability | SHAP + custom rule-based | Per-prediction feature importance |

## Model Performance

| Metric | Value | Threshold | Status |
|---|---|---|---|
| AUC-ROC | 0.847 | ≥ 0.80 | Pass |
| Precision (default class) | 0.72 | ≥ 0.65 | Pass |
| Recall (default class) | 0.68 | ≥ 0.60 | Pass |
| Demographic parity ratio | 0.91 | ≥ 0.85 | Pass |
| Equalized odds difference | 0.04 | ≤ 0.10 | Pass |
| Calibration error | 0.028 | ≤ 0.05 | Pass |

# Transparency and Information to Deployers (Article 13)

## User-Facing Information

All credit applicants receive the following information before the AI system processes their application:

1. **Notice of AI use** — Clear statement that an AI system is used in the credit assessment
2. **Input data** — Which categories of personal data are used in the assessment
3. **Output explanation** — Plain-language explanation of the credit score and key contributing factors
4. **Right to explanation** — Ability to request a detailed explanation of any individual decision
5. **Right to contest** — Process for challenging the AI-generated assessment and requesting human review
6. **Contact information** — Dedicated channel for AI-related inquiries

## Deployer Documentation

| Document | Audience | Content |
|---|---|---|
| Integration Guide | Technical teams | API specs, data format, error handling |
| Operational Manual | Risk managers | Monitoring procedures, escalation criteria, override guidelines |
| Bias Report | Compliance officers | Quarterly fairness metrics, identified issues, remediation actions |
| Incident Playbook | All deployers | Response procedures for model failures, bias incidents, data breaches |

# Human Oversight (Article 14)

## Oversight Mechanisms

| Mechanism | Description | Scope |
|---|---|---|
| Human-in-the-loop | Mandatory human review for all decline decisions > €5,000 | High-value decisions |
| Human-on-the-loop | Automated alerts for score anomalies, bias drift, model confidence < 0.7 | All decisions |
| Human-in-command | Kill switch to disable automated decisioning within 5 minutes | Emergency |
| Periodic audit | Random sample review (5% of decisions) by senior credit analysts | Ongoing |

## Override Authority

| Decision Value | AI Authority | Human Authority |
|---|---|---|
| ≤ €2,000 (approve) | Fully automated | Override available on request |
| ≤ €5,000 (approve) | Automated with notification | Override available on request |
| > €5,000 (approve) | Recommendation only | Human approval required |
| Any amount (decline) | Recommendation only | Human review mandatory within 48h |

# Accuracy, Robustness, and Cybersecurity (Article 15)

## Accuracy

- Model accuracy validated on held-out test set (20% stratified split) and quarterly production data
- Performance thresholds defined with automated alerts for degradation
- Fallback to rule-based scoring if model confidence drops below threshold

## Robustness

| Test | Method | Result |
|---|---|---|
| Adversarial robustness | Perturbation testing (±10% on numerical features) | Score change < 5% |
| Distribution shift | Out-of-distribution detection via isolation forest | Detection rate > 95% |
| Missing data | Graceful degradation with imputation; alert if >3 features missing | Functional |
| Edge cases | Boundary value testing on all input features | No anomalous outputs |

## Cybersecurity

| Control | Implementation |
|---|---|
| API authentication | OAuth 2.0 + mTLS, API key rotation every 90 days |
| Input validation | JSON schema validation, range checks, anomaly detection |
| Model integrity | Signed model artifacts, checksum verification on deployment |
| Audit trail | Immutable log of all predictions, inputs, and model versions |
| Penetration testing | Annual third-party pentest; last completed April 2026 |

# Conformity Assessment Result

## Compliance Summary

| Requirement | Article | Status | Notes |
|---|---|---|---|
| Risk management system | Art. 9 | Compliant | Continuous process established |
| Data governance | Art. 10 | Compliant | Bias audit process operational |
| Technical documentation | Art. 11 | Compliant | Full documentation maintained |
| Record-keeping | Art. 12 | Compliant | Automated logging, 5-year retention |
| Transparency | Art. 13 | Compliant | User information and deployer docs complete |
| Human oversight | Art. 14 | Compliant | Multi-tier oversight implemented |
| Accuracy and robustness | Art. 15 | Compliant | Testing regime established |
| Quality management | Art. 17 | Compliant with conditions | Incident response procedures being enhanced (Q3 2026) |

## Conditions for Compliance

1. **Bias remediation** — The 3.2% age-based approval rate differential (R-01) must be reduced to within 2% by Q3 2026
2. **Incident response** — Enhanced AI incident response procedures must be formalized and tested by Q3 2026

## Declaration

This conformity assessment has been conducted in accordance with Article 43 of Regulation (EU) 2024/1689. The AI system described herein is found to be **compliant with conditions** with the requirements of Chapter 3 for high-risk AI systems.

| Role | Name | Signature | Date |
|---|---|---|---|
| Head of AI Governance | Dr. Maria Klein | | |
| Chief Risk Officer | Henrik Johansson | | |
| Data Protection Officer | Dr. Lisa Hofmann | | |
| Chief Technology Officer | Alessandro Rossi | | |
