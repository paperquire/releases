# Assessment Overview

## Organization Profile

| Field | Detail |
|---|---|
| Organization | NordGrid Energie GmbH |
| Sector | Energy — Electricity distribution |
| NIS2 Classification | Essential Entity (Annex I, Sector 1: Energy) |
| Member State | Germany |
| Competent Authority | BSI (Bundesamt für Sicherheit in der Informationstechnik) |
| Assessment Date | June 25, 2026 |
| Assessor | Internal Cybersecurity Team + External Auditor (TÜV Rheinland) |
| Regulatory Basis | Directive (EU) 2022/2555 (NIS2), transposed via NIS2UmsuCG (Germany) |

## Scope

This assessment covers all network and information systems that support the essential services provided by NordGrid Energie GmbH, including:

- Electricity distribution network (SCADA/OT systems)
- Customer management and billing systems
- Corporate IT infrastructure
- Supply chain ICT dependencies

> [!important]
> As an essential entity under NIS2, NordGrid is subject to the full requirements of Article 21 (cybersecurity risk management measures) and Article 23 (incident reporting obligations), with supervisory oversight by BSI.

# Governance and Accountability (Article 20)

## Management Body Obligations

The management body (Geschäftsführung) is required under Article 20 to:

- [x] Approve cybersecurity risk management measures
- [x] Oversee implementation of security measures
- [x] Complete cybersecurity training (last completed: March 2026)
- [x] Be held accountable for non-compliance
- [x] Ensure adequate resources for cybersecurity

## Cybersecurity Organization

| Role | Name | Responsibility | Reporting Line |
|---|---|---|---|
| Chief Information Security Officer | Dr. Stefan Müller | Overall cybersecurity program | CEO (direct) |
| OT Security Manager | Katrin Bauer | SCADA/ICS security, OT monitoring | CISO |
| IT Security Manager | Michael Schmidt | Corporate IT security, IAM, endpoint | CISO |
| Incident Response Lead | Julia Fischer | SOC operations, incident handling | CISO |
| Compliance Manager | Andreas Weber | NIS2/BSI compliance, audit coordination | CISO |
| Third-Party Risk Analyst | Sarah Klein | Supply chain cybersecurity assessment | CISO |

# Cybersecurity Risk Management Measures (Article 21)

## Article 21(2)(a): Risk Analysis and Information System Security Policies

### Risk Assessment Methodology

| Element | Approach |
|---|---|
| Framework | ISO 27005:2022, aligned with BSI IT-Grundschutz |
| Scope | IT and OT systems supporting essential services |
| Assessment frequency | Annual comprehensive + continuous monitoring |
| Risk appetite | Defined by management body; zero tolerance for risks to public safety |

### Current Risk Posture

| Risk Category | Identified Risks | High | Medium | Low | Accepted |
|---|---|---|---|---|---|
| OT/SCADA security | 12 | 2 | 7 | 3 | 0 |
| IT infrastructure | 18 | 1 | 8 | 9 | 2 |
| Third-party / supply chain | 8 | 2 | 4 | 2 | 0 |
| Human factors | 6 | 0 | 3 | 3 | 1 |
| Physical security | 4 | 0 | 1 | 3 | 1 |
| **Total** | **48** | **5** | **23** | **20** | **4** |

### Security Policies

| Policy | Version | Last Review | Next Review | Owner |
|---|---|---|---|---|
| Information Security Policy | 4.0 | January 2026 | January 2027 | CISO |
| OT/ICS Security Policy | 2.1 | March 2026 | March 2027 | OT Security Manager |
| Access Control Policy | 3.2 | February 2026 | February 2027 | IT Security Manager |
| Incident Response Policy | 3.0 | April 2026 | October 2026 | IR Lead |
| Third-Party Security Policy | 2.0 | January 2026 | January 2027 | Third-Party Risk Analyst |
| Acceptable Use Policy | 2.5 | November 2025 | November 2026 | IT Security Manager |

## Article 21(2)(b): Incident Handling

### Incident Response Capability

| Capability | Status | Detail |
|---|---|---|
| 24/7 SOC | Operational | Internal SOC (3 shifts) + MSSP overflow |
| Incident classification | Implemented | 4-tier severity, aligned with BSI/ENISA taxonomy |
| Response playbooks | 14 documented | Covering ransomware, DDoS, OT intrusion, data breach, insider threat |
| Forensic capability | Internal + retainer | In-house for first response; CrowdStrike on retainer for complex cases |
| Communication plan | Documented | Internal, BSI, media, and customer notification procedures |

### NIS2 Incident Reporting (Article 23)

| Report | Deadline | Channel | Content |
|---|---|---|---|
| Early warning | 24 hours | BSI portal | Suspected significant incident, initial indicators |
| Incident notification | 72 hours | BSI portal | Initial assessment, severity, impact, cross-border indicators |
| Intermediate report | Upon BSI request | BSI portal | Updated status, containment measures |
| Final report | 1 month | BSI portal | Root cause, full impact, remediation, lessons learned |

### Incident Statistics (January–June 2026)

| Category | Count | Significant (NIS2) | BSI Reported |
|---|---|---|---|
| Malware/ransomware | 3 | 0 | 0 |
| Phishing/social engineering | 28 | 0 | 0 |
| Unauthorized access attempts | 156 | 1 | 1 |
| DDoS | 2 | 0 | 0 |
| OT security events | 4 | 0 | 0 |
| Data incidents | 1 | 0 | 0 |

## Article 21(2)(c): Business Continuity and Crisis Management

| Element | Status | Detail |
|---|---|---|
| Business continuity plan | Current | Covers all essential services; tested semi-annually |
| Disaster recovery | Current | Dual control centers (Hamburg, Hannover), 4-hour RTO for SCADA |
| Backup management | Compliant | 3-2-1 strategy, air-gapped OT backups, weekly restoration tests |
| Crisis management team | Established | CEO, CISO, CTO, Legal, Communications, Operations |
| Crisis communication | Documented | BSI, CERT-Bund, sector ISAC, media response templates |

## Article 21(2)(d): Supply Chain Security

### Critical Suppliers Assessment

| Supplier | Service | Criticality | Security Assessment | Last Audit | Compliant |
|---|---|---|---|---|---|
| Siemens Energy | SCADA/EMS software | Critical | On-site audit + SOC 2 | March 2026 | Yes |
| SAP | ERP and billing | Critical | SOC 2 Type II + pentest | January 2026 | Yes |
| Deutsche Telekom | WAN connectivity | Critical | ISO 27001 certified | February 2026 | Yes |
| AWS | Cloud hosting (IT systems) | Important | SOC 2 + C5 attestation | Continuous | Yes |
| Schneider Electric | Substation automation | Important | Security questionnaire | April 2026 | Partial — action plan agreed |

> [!warning]
> Schneider Electric's substation automation firmware update process does not meet NordGrid's secure development lifecycle requirements. A remediation plan has been agreed with a target completion of Q4 2026. Interim compensating controls (network isolation, enhanced monitoring) are in place.

### Supply Chain Risk Measures

- Cybersecurity requirements in all procurement contracts
- Right-to-audit clauses for critical suppliers
- Annual security assessment of critical suppliers
- Software bill of materials (SBOM) required for all OT software
- Vulnerability disclosure coordination with vendors

## Article 21(2)(e): Security in Network and Information System Acquisition, Development, and Maintenance

| Control | OT Systems | IT Systems |
|---|---|---|
| Secure development lifecycle | Vendor requirement (IEC 62443) | Internal SSDLC + SAST/DAST |
| Vulnerability management | Monthly scanning, quarterly patching windows | Weekly scanning, automated patching |
| Change management | CAB approval, OT test environment validation | CI/CD with automated security gates |
| Configuration management | CIS benchmarks + IEC 62443 baselines | CIS benchmarks, automated compliance |

## Article 21(2)(f): Policies and Procedures for Assessing Effectiveness

| Assessment | Frequency | Scope | Last Performed |
|---|---|---|---|
| Internal audit | Annual | Full NIS2 scope | April 2026 |
| External audit | Biannual | Essential service systems | March 2026 (TÜV) |
| Penetration testing — IT | Annual | External perimeter + critical apps | May 2026 |
| Penetration testing — OT | Annual | SCADA network (isolated lab) | February 2026 |
| Red team exercise | Biannual | Enterprise-wide (IT + OT) | November 2025 |
| Tabletop exercise | Quarterly | Incident response scenarios | May 2026 |

## Article 21(2)(g): Cybersecurity Training and Cyber Hygiene

| Program | Audience | Frequency | Completion Rate |
|---|---|---|---|
| Security awareness training | All employees (820) | Quarterly | 97% |
| Phishing simulation | All employees | Monthly | 94% pass rate |
| Management body training | Geschäftsführung (4) | Annual | 100% |
| OT-specific security training | OT engineers (45) | Semi-annual | 100% |
| Incident response training | SOC + IR team (12) | Quarterly | 100% |
| Secure coding training | Development team (22) | Annual | 100% |

## Article 21(2)(h): Cryptography and Encryption

| Domain | Standard | Implementation |
|---|---|---|
| Data at rest (IT) | AES-256 | Full disk encryption, database TDE |
| Data at rest (OT) | AES-256 where supported | Historian databases, configuration backups |
| Data in transit (IT) | TLS 1.3 | All internal and external communications |
| Data in transit (OT) | IEC 62351 / TLS 1.2+ | SCADA communications, inter-substation links |
| Key management | HSM-based | Thales Luna HSM for PKI and signing keys |
| Certificate management | Automated | HashiCorp Vault, 90-day rotation for IT certificates |

## Article 21(2)(i): Human Resources Security and Access Control

| Control | Implementation |
|---|---|
| Background checks | All employees and contractors with access to critical systems |
| Least privilege access | Role-based access control, quarterly access reviews |
| Privileged access management | CyberArk PAM for all administrative access |
| MFA | Required for all systems (FIDO2 for OT access) |
| Joiner/mover/leaver process | Automated via HR system integration, 24-hour SLA for revocation |
| Physical access control | Biometric + badge for control centers, logged and reviewed |

## Article 21(2)(j): Multi-Factor Authentication and Secure Communication

| System | MFA Method | Secure Communication |
|---|---|---|
| Corporate IT | FIDO2 security keys + Okta | TLS 1.3, encrypted email (S/MIME) |
| OT/SCADA access | Hardware tokens + certificate-based | Encrypted VPN, dedicated OT network |
| Remote access | FIDO2 + device certificates | Zero-trust network access (ZTNA) |
| Emergency communication | Pre-shared keys + out-of-band verification | Encrypted satellite phone + Signal |

# Compliance Summary

| Article 21(2) Requirement | Status | Maturity (1–5) | Gap |
|---|---|---|---|
| (a) Risk analysis and policies | Compliant | 4 | — |
| (b) Incident handling | Compliant | 4 | — |
| (c) Business continuity | Compliant | 4 | — |
| (d) Supply chain security | Partially compliant | 3 | Schneider Electric remediation pending |
| (e) Acquisition and development | Compliant | 4 | — |
| (f) Effectiveness assessment | Compliant | 4 | — |
| (g) Training and cyber hygiene | Compliant | 5 | — |
| (h) Cryptography | Compliant | 4 | — |
| (i) HR security and access control | Compliant | 4 | — |
| (j) MFA and secure communications | Compliant | 4 | — |

**Overall Assessment**: **Compliant** — One partial compliance item (supply chain) with agreed remediation timeline. No critical gaps identified.
