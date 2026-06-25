# Executive Summary

Acme Corp's customer onboarding process currently takes an average of 14 business days, resulting in a 23% drop-off rate before first value delivery. This Business Requirements Document defines the requirements for a self-service onboarding portal that reduces time-to-value to under 2 business days and improves new customer retention by 15%.

# Business Context

## Current State

New customers are onboarded through a manual process involving email exchanges, PDF form submissions, and scheduled setup calls with the implementation team. Key pain points:

- **14-day average onboarding time** (industry benchmark: 3 days)
- **23% abandonment rate** during onboarding
- **3.2 FTE** dedicated to manual onboarding tasks
- **No self-service option** for standard configurations

## Desired State

A web-based self-service portal that guides customers through account setup, configuration, data import, and first-use workflows with minimal human intervention.

## Business Drivers

| Driver | Priority | Metric |
|---|---|---|
| Reduce time-to-value | Critical | Onboarding time < 2 days |
| Improve retention | High | First-90-day churn < 5% |
| Reduce support burden | High | Onboarding tickets < 10/week |
| Enable self-service | Medium | 80% of customers self-onboard |

# Stakeholder Analysis

| Stakeholder | Role | Interest | Influence |
|---|---|---|---|
| VP Sales | Sponsor | Faster deal-to-revenue cycle | High |
| Head of CS | Key stakeholder | Reduce team workload | High |
| Product Manager | Requirements owner | Feature prioritization | Medium |
| Engineering Lead | Technical feasibility | Architecture fit | Medium |
| Legal/Compliance | Reviewer | Data handling, consent flows | Low |

# Functional Requirements

## FR-1: Account Setup

The system shall allow new customers to create their organization account through a guided wizard that collects:

- Organization name, industry, and size
- Primary administrator details
- Billing information (credit card or invoice)
- Service tier selection

### Acceptance Criteria

- [ ] User can complete account creation in under 5 minutes
- [ ] Email verification is required before proceeding
- [ ] Duplicate organization detection with merge suggestion
- [ ] SSO configuration available for Enterprise tier

## FR-2: Configuration Wizard

The system shall provide a step-by-step configuration wizard tailored to the customer's industry and tier:

| Step | Description | Required |
|---|---|---|
| 1. Workspace Setup | Name workspace, invite team members | Yes |
| 2. Integration Connect | Connect existing tools (CRM, ERP) | No |
| 3. Data Import | Upload CSV or connect API source | No |
| 4. Branding | Upload logo, set brand colors | No |
| 5. First Workflow | Create first automated workflow from template | Yes |

## FR-3: Progress Tracking

The system shall display onboarding progress to both the customer and internal teams:

- Visual progress bar with completed/remaining steps
- Estimated time to complete remaining steps
- Ability to skip optional steps and return later
- Automated nudge emails for stalled onboarding (24h, 72h, 7d)

## FR-4: Guided Tours

The system shall provide contextual in-app guidance:

- Interactive product tours triggered on first visit to each feature area
- Tooltip-based hints for complex UI elements
- Video tutorials embedded at relevant steps
- Searchable knowledge base with auto-suggested articles

# Non-Functional Requirements

| Requirement | Specification |
|---|---|
| Availability | 99.9% uptime during business hours |
| Performance | Page load < 2s, API response < 500ms |
| Scalability | Support 500 concurrent onboarding sessions |
| Security | SOC 2 compliant, data encrypted at rest and in transit |
| Accessibility | WCAG 2.1 AA compliance |
| Browser Support | Chrome, Firefox, Safari, Edge (latest 2 versions) |

# Constraints and Assumptions

## Constraints

- Must integrate with existing Salesforce CRM for lead-to-customer handoff
- Cannot modify the core billing system (API-only integration)
- Must launch before Q4 sales season (October 1 deadline)

## Assumptions

- Customers have modern web browsers with JavaScript enabled
- SSO integration is only required for Enterprise tier
- Data import templates will be standardized (no custom formats in v1)

> [!note]
> The MVP scope excludes multi-language support. Localization is planned for v2 based on international expansion timeline.

# Success Metrics

| Metric | Current | Target | Measurement |
|---|---|---|---|
| Onboarding time (median) | 14 days | < 2 days | Time from signup to first workflow |
| Abandonment rate | 23% | < 8% | Users who don't complete setup in 30 days |
| Support tickets (onboarding) | 45/week | < 10/week | Zendesk category filter |
| Self-service rate | 0% | > 80% | Completed without human intervention |
| First-90-day retention | 82% | > 95% | Cohort analysis |
