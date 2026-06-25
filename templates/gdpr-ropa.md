# Overview

## Controller Information

| Field | Detail |
|---|---|
| Organization | Nexus Solutions GmbH |
| Registration Number | HRB 123456 |
| Registered Address | Friedrichstraße 123, 10117 Berlin, Germany |
| Data Protection Officer | Dr. Lisa Hofmann, dpo@nexus-solutions.eu, +49 30 1234 5678 |
| EU Representative (if applicable) | N/A (established in EU) |
| Date of Last Update | June 25, 2026 |
| Version | 3.1 |

## Purpose of This Register

This document constitutes the Records of Processing Activities maintained in accordance with Article 30(1) of the General Data Protection Regulation (EU) 2016/679. It documents all processing activities involving personal data carried out by Nexus Solutions GmbH as data controller.

> [!important]
> This register must be made available to the supervisory authority (Berliner Beauftragte für Datenschutz und Informationsfreiheit) upon request. All departments are responsible for reporting new processing activities or changes to the DPO within 5 business days.

# Processing Activities Register

## PA-001: Customer Relationship Management

| Field | Detail |
|---|---|
| Processing Activity | Customer account management and commercial relationship |
| Department | Sales & Customer Success |
| Purpose | Contract performance, billing, account management, customer communication |
| Legal Basis | Art. 6(1)(b) — Performance of contract |
| Categories of Data Subjects | Business customers (primary contacts, billing contacts, end users) |
| Categories of Personal Data | Name, email, phone, company, job title, billing address, payment information (tokenized) |
| Special Category Data | None |
| Source of Data | Directly from data subjects (registration, contract) |
| Recipients | Internal: Sales, CS, Finance · External: Stripe (payment processing), Salesforce (CRM) |
| Cross-border Transfers | Salesforce (US) — SCCs Module 2; Stripe (US) — SCCs Module 2 |
| Retention Period | Duration of contract + 10 years (German commercial retention: §257 HGB) |
| Technical Measures | Encryption at rest (AES-256), TLS 1.3, access control, audit logging |
| Organizational Measures | Need-to-know access, quarterly access reviews, data processing agreements |
| DPIA Required | No |
| Last Review | March 2026 |

## PA-002: Employee Data Processing

| Field | Detail |
|---|---|
| Processing Activity | Human resources management and payroll |
| Department | People Operations |
| Purpose | Employment contract performance, payroll, benefits administration, legal obligations |
| Legal Basis | Art. 6(1)(b) — Employment contract · Art. 6(1)(c) — Legal obligation (tax, social security) |
| Categories of Data Subjects | Employees, contractors, job applicants |
| Categories of Personal Data | Name, address, date of birth, tax ID, social security number, bank details, salary, performance reviews |
| Special Category Data | Health data (sick leave certificates) — Art. 9(2)(b) employment law obligation |
| Source of Data | Directly from data subjects, public authorities (tax office) |
| Recipients | Internal: HR, Finance · External: DATEV (payroll), health insurance providers, tax authorities |
| Cross-border Transfers | None (all processors EU-based) |
| Retention Period | Duration of employment + 10 years (§257 HGB, §147 AO) |
| Technical Measures | Encrypted HR system, MFA, dedicated access controls, encrypted backup |
| Organizational Measures | HR staff confidentiality agreements, locked physical records, restricted system access |
| DPIA Required | No |
| Last Review | January 2026 |

## PA-003: Website Analytics

| Field | Detail |
|---|---|
| Processing Activity | Website visitor analytics and conversion tracking |
| Department | Marketing |
| Purpose | Website performance analysis, conversion optimization, marketing attribution |
| Legal Basis | Art. 6(1)(a) — Consent (via cookie banner) |
| Categories of Data Subjects | Website visitors |
| Categories of Personal Data | IP address (anonymized after collection), device type, browser, pages visited, referral source, conversion events |
| Special Category Data | None |
| Source of Data | Automatically collected via analytics scripts (consent required) |
| Recipients | Internal: Marketing · External: Plausible Analytics (EU-hosted) |
| Cross-border Transfers | None (Plausible hosted in EU) |
| Retention Period | 26 months (aggregated data only; raw data deleted after 30 days) |
| Technical Measures | IP anonymization, cookieless tracking option, TLS, access control |
| Organizational Measures | Consent management platform, regular consent audit, privacy-by-design analytics |
| DPIA Required | No |
| Last Review | April 2026 |

## PA-004: Product Behavioral Analytics

| Field | Detail |
|---|---|
| Processing Activity | In-product user behavior analysis and personalization |
| Department | Product |
| Purpose | Product improvement, churn prediction, personalized user experience |
| Legal Basis | Art. 6(1)(f) — Legitimate interest (product improvement) · Art. 6(1)(a) — Consent (personalization) |
| Categories of Data Subjects | Product end users (~45,000) |
| Categories of Personal Data | User ID, email, IP, device info, feature usage, clickstream, engagement scores |
| Special Category Data | None |
| Source of Data | Automatically collected during product use |
| Recipients | Internal: Product, CS, Marketing · External: Mixpanel (US), Snowflake (EU) |
| Cross-border Transfers | Mixpanel (US) — SCCs Module 2 + supplementary measures |
| Retention Period | Raw events: 90 days · Profiles: 2 years · ML outputs: 1 year |
| Technical Measures | Pseudonymization, encryption, input field masking, automated deletion |
| Organizational Measures | DPIA completed, consent mechanism, bias audits for ML models |
| DPIA Required | **Yes — completed June 2026** |
| Last Review | June 2026 |

## PA-005: Recruitment

| Field | Detail |
|---|---|
| Processing Activity | Job applicant management |
| Department | People Operations |
| Purpose | Recruitment process, applicant evaluation, talent pool management |
| Legal Basis | Art. 6(1)(b) — Pre-contractual measures · Art. 6(1)(a) — Consent (talent pool) |
| Categories of Data Subjects | Job applicants |
| Categories of Personal Data | Name, email, phone, CV/resume, cover letter, interview notes, assessment results |
| Special Category Data | None (disability status only if voluntarily disclosed, Art. 9(2)(a)) |
| Source of Data | Directly from applicants, LinkedIn (with consent), recruitment agencies |
| Recipients | Internal: HR, hiring managers · External: Personio (ATS, EU-hosted) |
| Cross-border Transfers | None |
| Retention Period | Active applications: duration of process + 6 months · Talent pool: 2 years (with consent renewal) |
| Technical Measures | ATS access controls, encrypted storage, audit logging |
| Organizational Measures | Hiring manager data access training, structured interview process, deletion reminders |
| DPIA Required | No |
| Last Review | February 2026 |

## PA-006: Security Monitoring and Incident Response

| Field | Detail |
|---|---|
| Processing Activity | IT security monitoring, log analysis, and incident investigation |
| Department | Information Security |
| Purpose | Protecting systems and data from security threats, legal obligations |
| Legal Basis | Art. 6(1)(f) — Legitimate interest · Art. 6(1)(c) — Legal obligation (NIS2) |
| Categories of Data Subjects | Employees, contractors, system administrators |
| Categories of Personal Data | Usernames, IP addresses, access logs, authentication events, email metadata |
| Special Category Data | None |
| Source of Data | Automatically collected from IT systems |
| Recipients | Internal: Security team · External: Splunk (SIEM, EU-hosted), CrowdStrike (EDR, US — SCCs) |
| Cross-border Transfers | CrowdStrike (US) — SCCs Module 2 |
| Retention Period | Security logs: 2 years · Incident records: 5 years |
| Technical Measures | WORM storage, encryption, privileged access management, network segmentation |
| Organizational Measures | Security clearance for SOC analysts, incident response procedures, log review schedule |
| DPIA Required | No |
| Last Review | May 2026 |

# Cross-Border Transfer Summary

| Recipient | Country | Transfer Mechanism | Supplementary Measures | SCC Review Date |
|---|---|---|---|---|
| Salesforce | US | SCCs (Module 2) | Encryption, access controls | January 2026 |
| Stripe | US | SCCs (Module 2) | Tokenization, PCI DSS | January 2026 |
| Mixpanel | US | SCCs (Module 2) | Encryption, pseudonymization | February 2026 |
| CrowdStrike | US | SCCs (Module 2) | Encryption, minimal data | March 2026 |

> [!note]
> All SCCs are based on the European Commission's Standard Contractual Clauses adopted by Implementing Decision (EU) 2021/914. Transfer Impact Assessments (TIAs) are conducted annually for each US-based sub-processor.

# Review Schedule

| Processing Activity | Next Review | Responsible |
|---|---|---|
| PA-001: CRM | September 2026 | Head of Sales |
| PA-002: Employee Data | January 2027 | Head of HR |
| PA-003: Website Analytics | October 2026 | Head of Marketing |
| PA-004: Product Analytics | December 2026 | Head of Product |
| PA-005: Recruitment | August 2026 | Head of HR |
| PA-006: Security Monitoring | November 2026 | CISO |

# Document Control

| Version | Date | Author | Changes |
|---|---|---|---|
| 3.1 | June 25, 2026 | Dr. Lisa Hofmann | Added PA-004 DPIA reference, updated sub-processor list |
| 3.0 | January 15, 2026 | Dr. Lisa Hofmann | Annual review, added PA-006 |
| 2.0 | June 20, 2025 | Dr. Lisa Hofmann | Added cross-border transfer section, NIS2 references |
| 1.0 | January 10, 2025 | Dr. Lisa Hofmann | Initial version |
