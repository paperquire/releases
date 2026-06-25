# Document Control

## Document Information

| Field | Detail |
|---|---|
| Document Title | ICT Risk Management Framework |
| Organization | EuroBank Digital AG |
| Regulatory Basis | Regulation (EU) 2022/2554 (DORA) — Articles 5–16 |
| Applicable From | January 17, 2025 |
| Document Version | 2.0 |
| Classification | Confidential |
| Approved By | Management Body (Vorstand) |
| Last Review | June 25, 2026 |
| Next Review | December 2026 |

## Revision History

| Version | Date | Author | Changes |
|---|---|---|---|
| 2.0 | June 25, 2026 | ICT Risk Team | Added cloud concentration risk assessment, updated RTS references |
| 1.1 | March 15, 2026 | ICT Risk Team | Incorporated EBA/ESA Regulatory Technical Standards |
| 1.0 | January 10, 2025 | ICT Risk Team | Initial framework aligned with DORA requirements |

# ICT Risk Management Framework Overview

## Scope

This ICT Risk Management Framework applies to all information and communication technology (ICT) systems, processes, and third-party services that support the critical or important functions of EuroBank Digital AG. It is established in accordance with Article 6 of DORA and the associated Regulatory Technical Standards (RTS).

## Governance Structure

### Management Body Responsibilities (Article 5)

The Management Body (Vorstand) bears ultimate responsibility for the ICT risk management framework and shall:

1. Define, approve, and oversee the ICT risk management framework
2. Allocate adequate budget and resources for ICT risk management
3. Approve the ICT business continuity policy and ICT disaster recovery plans
4. Review and approve ICT audit plans and results
5. Undergo adequate ICT risk training at least annually

### ICT Risk Management Function

| Role | Responsibility | Reporting Line |
|---|---|---|
| Chief Information Security Officer (CISO) | Overall ICT risk management, framework maintenance | CRO → Management Body |
| Head of ICT Operations | Operational resilience, incident management | CTO → Management Body |
| ICT Risk Manager | Risk identification, assessment, monitoring | CISO → CRO |
| ICT Compliance Officer | Regulatory compliance, DORA alignment | CCO → Management Body |
| Third-Party Risk Manager | ICT third-party oversight, concentration risk | CISO → CRO |

> [!important]
> In accordance with Article 6(8), the ICT risk management function is independent from ICT operations and has direct reporting access to the Management Body. The CISO is not subordinate to the CTO.

# ICT Risk Identification (Article 8)

## ICT Asset Inventory

All ICT assets supporting critical or important functions are documented and classified:

| Asset Category | Count | Classification Method | Update Frequency |
|---|---|---|---|
| Business applications | 47 | BIA-based criticality (P1–P4) | Quarterly |
| Infrastructure components | 312 | Dependency mapping | Monthly |
| Data repositories | 28 | Data classification policy | Quarterly |
| Network segments | 14 | Zone-based security model | Semi-annually |
| ICT third-party services | 23 | DORA criticality assessment | Annually + trigger-based |

## Critical or Important Functions

| Function | Supporting Systems | RTO | RPO | Criticality |
|---|---|---|---|---|
| Core banking | T24, Oracle DB, ESB | 2 hours | 0 (synchronous replication) | Critical |
| Payment processing | SWIFT, SEPA gateway, fraud engine | 1 hour | 0 | Critical |
| Online banking | Web/mobile app, API gateway, IAM | 4 hours | 1 hour | Critical |
| Regulatory reporting | ABACUS, data warehouse | 8 hours | 4 hours | Important |
| Customer onboarding | KYC platform, document management | 24 hours | 8 hours | Important |
| Internal communication | Email, Teams, intranet | 8 hours | 4 hours | Standard |

## Risk Identification Methodology

Risks are identified through:

1. **Threat intelligence** — ENISA threat landscape, FS-ISAC feeds, BaFin advisories
2. **Vulnerability management** — Automated scanning (weekly), penetration testing (annual), red team exercises (biannual)
3. **Incident analysis** — Root cause analysis of all P1/P2 incidents, trend analysis quarterly
4. **Scenario analysis** — Annual ICT risk scenarios aligned with ECB/EBA expectations
5. **Change-driven assessment** — Risk assessment for all significant ICT changes

# ICT Risk Assessment and Treatment

## Risk Assessment Matrix

| | Negligible Impact | Minor Impact | Moderate Impact | Significant Impact | Severe Impact |
|---|---|---|---|---|---|
| **Almost Certain** | Medium | High | High | Critical | Critical |
| **Likely** | Low | Medium | High | High | Critical |
| **Possible** | Low | Low | Medium | High | High |
| **Unlikely** | Low | Low | Low | Medium | High |
| **Rare** | Low | Low | Low | Low | Medium |

## Current Risk Register (Top Risks)

| ID | Risk | Inherent Risk | Controls | Residual Risk | Treatment |
|---|---|---|---|---|---|
| ICT-01 | Ransomware attack on core banking | Critical | Network segmentation, EDR, immutable backups, staff training | Medium | Accept with monitoring |
| ICT-02 | Cloud provider outage (primary region) | High | Multi-region deployment, automated failover, contractual SLAs | Low | Mitigate |
| ICT-03 | ICT third-party concentration risk | High | Multi-vendor strategy, exit plans, escrow agreements | Medium | Mitigate (action plan) |
| ICT-04 | Insider threat / data exfiltration | High | DLP, PAM, behavioral analytics, background checks | Medium | Accept with monitoring |
| ICT-05 | API security vulnerability | High | API gateway, WAF, DAST/SAST in CI/CD, bug bounty | Low | Mitigate |
| ICT-06 | Legacy system failure (T24 v15) | Medium | Upgrade plan (2027), enhanced monitoring, documented workarounds | Medium | Mitigate (scheduled) |

# ICT Incident Management (Articles 17–23)

## Incident Classification

| Severity | Criteria | Response Time | Escalation | DORA Reporting |
|---|---|---|---|---|
| Critical | Core banking / payments unavailable, data breach affecting >10K customers | Immediate | CISO + CTO + Management Body within 30 min | Initial notification to BaFin within 4 hours |
| Major | Significant degradation, data breach <10K customers | 30 minutes | CISO within 1 hour | Initial notification within 24 hours |
| Significant | Partial service disruption, no data breach | 2 hours | ICT Risk Manager | Reported in periodic summary |
| Minor | Isolated issue, workaround available | 4 hours | Team lead | Internal log only |

## Major ICT Incident Reporting (Article 19)

For incidents classified as major per DORA criteria, the following reporting timeline applies:

| Report | Deadline | Recipient | Content |
|---|---|---|---|
| Initial notification | 4 hours after classification | BaFin (via IMAS portal) | Incident type, impact, initial assessment |
| Intermediate report | 72 hours | BaFin | Updated impact, root cause analysis, containment measures |
| Final report | 1 month | BaFin | Full root cause, remediation actions, lessons learned |

## Incident Summary (January–June 2026)

| Severity | Count | Avg Resolution | SLA Met | DORA Reported |
|---|---|---|---|---|
| Critical | 0 | — | — | — |
| Major | 2 | 3h 45m | Yes | Yes (2 reports filed) |
| Significant | 8 | 6h 20m | Yes | N/A |
| Minor | 47 | 12h 15m | 94% | N/A |

# ICT Business Continuity (Articles 11–12)

## Business Continuity Policy

The ICT business continuity policy ensures the resilience of critical functions through:

1. **Redundancy** — All critical systems deployed across two data centers (Frankfurt, Dublin) with synchronous replication
2. **Recovery** — Documented disaster recovery procedures tested semi-annually
3. **Communication** — Crisis communication plan with defined roles, channels, and escalation paths
4. **Review** — Business Impact Analysis refreshed annually; BCP tested quarterly

## Recovery Capabilities

| Function | Recovery Strategy | RTO Target | RTO Tested | RPO Target | RPO Tested |
|---|---|---|---|---|---|
| Core banking | Active-active, synchronous replication | 2 hours | 1h 42m | 0 | 0 |
| Payments | Active-passive with automated failover | 1 hour | 48 min | 0 | 0 |
| Online banking | Multi-region, DNS failover | 4 hours | 2h 15m | 1 hour | 35 min |
| Regulatory reporting | Warm standby, async replication | 8 hours | 5h 30m | 4 hours | 2h 10m |

> [!note]
> The last full DR test was conducted on April 12, 2026. All critical functions met their RTO/RPO targets. Two improvement actions were identified and are tracked in the remediation register.

# ICT Third-Party Risk Management (Articles 28–30)

## Critical ICT Third-Party Providers

| Provider | Service | Criticality | Substitutability | Contract End | Exit Plan |
|---|---|---|---|---|---|
| AWS | Cloud infrastructure | Critical | Medium (multi-cloud strategy) | December 2028 | Documented, tested annually |
| Finastra | Core banking (T24) | Critical | Low | December 2029 | Documented, 18-month execution |
| SWIFT | Payment messaging | Critical | Low (industry standard) | Ongoing | Limited alternatives documented |
| Microsoft | Office 365, Azure AD | Important | Medium | March 2028 | Migration plan to alternative exists |
| CrowdStrike | Endpoint detection | Important | High | June 2027 | 90-day migration to alternative |

## Concentration Risk Assessment

| Dimension | Assessment | Risk Level |
|---|---|---|
| Cloud provider concentration | 78% of workloads on AWS | Medium — multi-cloud strategy in progress |
| Geographic concentration | Primary: Frankfurt, DR: Dublin | Low — two-region deployment |
| Technology concentration | Single core banking vendor (Finastra) | High — documented with Management Body |
| Sub-outsourcing chains | 3 providers with material sub-outsourcing | Medium — quarterly sub-outsourcing reviews |

## Contractual Requirements (Article 30)

All ICT third-party contracts for critical or important functions include:

- [x] Service level descriptions with quantitative metrics
- [x] Data location and processing requirements
- [x] Audit and access rights (including for competent authorities)
- [x] ICT incident notification obligations (alignment with DORA timelines)
- [x] Business continuity and exit strategy provisions
- [x] Sub-outsourcing consent and notification requirements
- [x] Termination rights for non-compliance

# Digital Operational Resilience Testing (Articles 24–27)

## Testing Program

| Test Type | Scope | Frequency | Last Performed | Next Scheduled |
|---|---|---|---|---|
| Vulnerability scanning | All externally facing systems | Weekly (automated) | June 24, 2026 | June 28, 2026 |
| Penetration testing | Critical applications and infrastructure | Annually | April 2026 | April 2027 |
| Threat-Led Penetration Testing (TLPT) | Core banking and payment systems | Every 3 years (Art. 26) | Not yet required | 2027 (first cycle) |
| DR/BCP testing | All critical functions | Semi-annually | April 2026 | October 2026 |
| Table-top exercises | Incident response and crisis management | Quarterly | May 2026 | August 2026 |
| Red team exercise | Enterprise-wide | Biannually | November 2025 | November 2026 |

> [!warning]
> Threat-Led Penetration Testing (TLPT) under Article 26 will be required for the first time in 2027. The procurement process for a qualified TLPT provider should begin in Q4 2026 to ensure readiness.

# Compliance Status and Action Plan

| DORA Article | Requirement | Status | Gap | Remediation Target |
|---|---|---|---|---|
| Art. 5–6 | ICT governance and risk framework | Compliant | — | — |
| Art. 7 | ICT systems, protocols, and tools | Compliant | — | — |
| Art. 8 | Identification | Compliant | — | — |
| Art. 9 | Protection and prevention | Compliant | Legacy system hardening needed | Q1 2027 |
| Art. 10 | Detection | Compliant | — | — |
| Art. 11–12 | Business continuity | Compliant | — | — |
| Art. 13 | Learning and evolving | Compliant | — | — |
| Art. 17–23 | Incident management and reporting | Compliant | BaFin portal integration in progress | Q3 2026 |
| Art. 24–27 | Resilience testing | Partially compliant | TLPT not yet performed | 2027 |
| Art. 28–30 | Third-party risk | Compliant | Concentration risk mitigation ongoing | Q4 2026 |
