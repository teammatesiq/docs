---
Document title: TeamMates Product Requirements Document
Version: 1.0
Status: Draft
Owner: TeamMates
Last updated: 2026-08-08
---

# 1. Purpose

This document defines the vision, target customer, scope, functional requirements, non-functional requirements, governance model and success criteria for the first TeamMates product: Admin TeamMate.

It is the primary product source of truth for Product, UX, Architecture and Engineering.

# 2. Product Vision

TeamMates provides governed digital colleagues that take meaningful repeatable work off human teams while keeping people in control of important decisions.

Admin TeamMate is the first commercial TeamMate for the UK SME v1 MVP (P-001).

It is not a generic chatbot or open-ended AI assistant.

It is a digital colleague with:

- a defined role
- clear responsibilities
- explicit permissions
- persistent organisational context
- governed workflows
- human approvals
- traceable actions
- controlled learning

# 3. Initial Market

Primary market:

- United Kingdom
- SMEs with approximately 5–50 employees
- Microsoft 365 users
- Knowledge-based and service-led businesses

Primary buyers:

- Founder
- Managing Director
- Operations Director
- Office Manager
- Business Owner

The strongest initial customer is an organisation where senior people still spend material time on repetitive administration.

# 4. Customer Problem

SME owners and managers spend significant time:

- managing email
- preparing meetings
- chasing actions
- producing routine documents
- searching for information
- managing calendar commitments
- following up people
- remembering administrative tasks

The product objective is to remove administrative work rather than simply make AI available.

# 5. Product Positioning

Customer-facing proposition:

> Hire digital colleagues that take real work off your team.

For the first product:

> Admin TeamMate keeps on top of your email, meetings, actions and routine admin.

Avoid positioning the product primarily as:

- AI software
- chatbot
- agent platform
- automation software
- Copilot replacement

# 6. Product Principles

Every TeamMate must:

1. Have a clearly defined role.
2. Operate within explicit permissions.
3. Keep humans accountable for important decisions.
4. Never silently bypass approval.
5. Distinguish fact from assumption.
6. Surface uncertainty.
7. Use approved organisational evidence.
8. Maintain traceability.
9. Learn customer preferences without weakening governance.
10. Reduce work rather than create additional administration.

# 7. Admin TeamMate Core Outcomes

Admin TeamMate exists to:

## 7.1 Control the Inbox

Help the user understand what requires attention without manually processing every message.

## 7.2 Improve Preparedness

Surface meetings, commitments and deadlines before they become problems.

## 7.3 Reduce Repetitive Writing

Prepare routine communications and documents.

## 7.4 Improve Follow-Through

Reduce forgotten actions and commitments.

## 7.5 Reduce Administrative Cognitive Load

Reduce the amount of remembering, searching, organising and chasing required from the customer.

# 8. MVP Capabilities

The MVP contains six primary customer capabilities.

## 8.1 Email Support

Admin TeamMate shall:

- read authorised email
- classify email priority
- identify messages requiring attention
- summarise email threads
- draft responses
- identify unanswered important messages

During MVP, external sending requires explicit human approval.

## 8.2 Meeting Support

Admin TeamMate shall:

- read authorised calendar information
- identify meetings requiring preparation
- prepare agendas
- prepare briefing notes
- surface relevant correspondence
- surface open actions
- prepare meeting follow-up from available notes or transcripts

## 8.3 Action Management

Admin TeamMate shall:

- capture actions
- preserve source
- track owner
- track due date
- identify overdue actions
- prepare follow-up reminders

## 8.4 Document Preparation

Admin TeamMate shall prepare routine:

- letters
- briefing notes
- reports
- customer updates
- meeting summaries
- proposals from approved source information

## 8.5 Daily Briefing

Admin TeamMate shall prepare a concise daily view of:

- priorities
- meetings
- actions
- deadlines
- pending approvals
- prepared work
- relevant recommendations

## 8.6 Knowledge Retrieval

Admin TeamMate shall search authorised organisational knowledge and return evidence-based answers with source references where practical.

# 9. Explicit MVP Exclusions

The MVP does not include:

- accounting
- payroll
- payment execution
- financial approval
- autonomous contract acceptance
- HR decision-making
- recruitment decision-making
- marketing automation
- sales strategy
- CRM ownership
- voice calling
- social-media execution
- unrestricted autonomous external action
- multi-TeamMate collaboration
- marketplace
- custom workflow builder
- native mobile application

# 10. Customer Journey

The target journey is:

Discover

→ Start Trial

→ Create Organisation

→ Hire Admin TeamMate

→ Connect Microsoft 365

→ Understand Permissions

→ Complete Business Interview

→ Select Approved Knowledge

→ Start Probation

→ Receive First Useful Work

→ Review and Approve Work

→ Experience Daily Value

→ Complete Probation

→ Subscribe

## 10.1 Deployed TeamMate Lifecycle

The canonical deployed TeamMate lifecycle is (D-001 / F-003):

Configuring → Probation → Active → Suspended → Archived

There is no Draft state for a deployed TeamMate. Draft remains valid only for definition assets where their own lifecycle explicitly includes it.

Customer-facing **Paused** maps to `status = suspended` with `suspension_reason = customer_paused`; it is not a separate lifecycle state. Other supported suspension reasons may include `trial_expired`, `subscription_suspended`, `security_suspension` and `admin_suspended`.

While Suspended, TMOS must not start new active execution or perform new controlled external actions, and must stop scheduled TeamMate work where appropriate. It must preserve durable workflow and task state, configuration, required audit history and customer data subject to applicable retention rules.

Reactivation must revalidate the relevant subscription or entitlement, integrations, permissions, policy and TeamMate configuration before active execution resumes.

# 11. Probation Model

Every new Admin TeamMate begins in Probation Mode.

Purpose:

- build trust
- validate integrations
- validate permissions
- learn preferences
- prevent premature autonomy

During probation:

- external actions require approval
- learning remains controlled
- behaviour is more explanatory
- uncertainty is surfaced
- no additional autonomy is granted automatically

Default probation duration is approximately seven calendar days, but completion is based on readiness rather than elapsed time alone.

# 12. Permission Model

Default capability classes:

## Read

Examples:

- email
- calendar
- selected documents
- approved knowledge

## Prepare

Examples:

- draft email
- draft document
- proposed action
- proposed meeting

## Approval Required

Examples:

- send external email
- create or modify meeting
- share documents externally
- assign work to another person

## Prohibited in MVP

Examples:

- make payment
- approve expense
- accept contract
- modify security
- grant permissions
- delete company information

# 13. Functional Requirements

FR-001  
The platform shall support secure organisation registration.

FR-002  
The platform shall authenticate users through supported identity providers.

FR-003  
Each organisation shall operate within an isolated tenant boundary.

FR-004  
The customer shall be able to deploy an Admin TeamMate.

FR-005  
Every deployed TeamMate shall have a defined role and version.

FR-006  
Every TeamMate shall operate under explicit permissions.

FR-007  
The platform shall support a probation state.

FR-008  
Admin TeamMate shall connect to Microsoft 365 through approved permissions.

FR-009  
Admin TeamMate shall be able to read authorised email.

FR-010  
Admin TeamMate shall be able to read authorised calendar information.

FR-011  
Admin TeamMate shall classify relevant email.

FR-012  
Admin TeamMate shall prepare email drafts.

FR-013  
External email sending shall require approval during MVP.

FR-014  
Admin TeamMate shall generate a Daily Briefing.

FR-015  
Admin TeamMate shall prepare meeting briefings.

FR-016  
Admin TeamMate shall maintain a structured action register.

FR-017  
Admin TeamMate shall prepare routine documents.

FR-018  
Admin TeamMate shall search approved organisational knowledge.

FR-019  
Knowledge retrieval shall preserve customer access boundaries.

FR-020  
Admin TeamMate shall surface missing or conflicting evidence.

FR-021  
Admin TeamMate shall request input where critical information is unavailable.

FR-022  
The platform shall maintain a customer-facing Work Queue.

FR-023  
The Work Queue shall expose Ready For You, Working, Needs Your Input and Completed states.

FR-024  
Approvals shall be first-class platform objects.

FR-025  
Approval history shall be traceable.

FR-026  
Permissions and policies shall be re-evaluated before controlled external execution.

FR-027  
The platform shall maintain an immutable audit history for meaningful actions.

FR-028  
Admin TeamMate shall support explicit customer-confirmed personalisation learning.

FR-029  
Personalisation shall not override governance or permissions.

FR-030  
The customer shall be able to pause or disconnect Admin TeamMate. Pausing shall apply the canonical Suspended state with `suspension_reason = customer_paused`.

# 14. Non-Functional Requirements

NFR-001 Security  
The system shall apply least-privilege access.

NFR-002 Tenant Isolation  
Customer data must not cross organisation boundaries.

NFR-003 Encryption  
Sensitive data shall be encrypted in transit and at rest.

NFR-004 Traceability  
Material TeamMate actions shall be reconstructable.

NFR-005 Resilience  
Temporary dependency failures shall fail safely.

NFR-006 Idempotency  
External actions vulnerable to duplication shall support idempotent execution.

NFR-007 Accessibility  
The web application shall target WCAG 2.2 AA.

NFR-008 Responsive UX  
Core review and approval experiences shall function on mobile web.

NFR-009 Observability  
Critical API, workflow, integration and reasoning behaviour shall be observable.

NFR-010 Provider Abstraction  
Core platform behaviour shall not depend directly on one AI model provider.

# 15. Trust Requirements

The customer must be able to understand:

- what the TeamMate can access
- what the TeamMate cannot access
- what requires approval
- what evidence supports work
- what the TeamMate has learned
- what actions have occurred
- how to pause the TeamMate
- how to disconnect integrations

Trust is a product requirement, not only a security requirement.

# 16. AI Behaviour Requirements

Admin TeamMate must:

- use approved context
- avoid unsupported claims
- avoid invented commitments
- distinguish explicit facts from inference
- expose ambiguity
- escalate low-confidence situations
- treat external content as data rather than authority
- resist prompt injection
- preserve system and organisational policy hierarchy

# 17. MVP Workflows

The MVP shall support:

WF-ADM-001 — Morning Briefing

WF-ADM-002 — Important Email

WF-ADM-003 — Meeting Preparation

WF-ADM-004 — Meeting Follow-Up

WF-ADM-005 — Overdue Action

WF-ADM-006 — Document Request

Supporting workflows include:

- Microsoft connection
- knowledge synchronisation
- approval execution
- learning proposal
- integration failure
- probation review

# 18. Success Metrics

## Activation

Customer:

- connects Microsoft 365
- completes onboarding
- activates Admin TeamMate
- completes or approves meaningful live-business work

## Usage

Customers should use Admin TeamMate repeatedly during the working week.

## Value

Target hypothesis:

At least 10 hours of administrative effort saved per customer per month once established.

## Quality

Target hypothesis:

At least 70% of routine prepared drafts accepted without significant rewrite during mature beta usage.

## Trust

Unexpected external action incidents should be exceptionally rare and treated as severe defects.

## Commercial

Key measures:

- trial activation
- trial-to-paid conversion
- monthly recurring revenue
- churn
- expansion demand
- willingness to add additional TeamMates

# 19. North Star Metric

Recommended North Star:

**Trusted Work Completed**

Examples:

- useful email drafts prepared
- meetings prepared
- documents produced
- actions managed
- workflows completed

The product should not optimise for:

- chat volume
- prompts
- tokens
- model calls

# 20. MVP Definition of Done

Admin TeamMate is ready for controlled SME beta when a customer can reliably:

1. Create an organisation.
2. Deploy Admin TeamMate.
3. Connect Microsoft 365.
4. Understand and configure permissions.
5. Complete onboarding.
6. Enter Probation Mode.
7. Receive a useful Daily Briefing.
8. Receive email prioritisation.
9. Review email drafts.
10. Approve controlled external actions.
11. Prepare for meetings.
12. Track actions.
13. Search approved knowledge.
14. Prepare routine documents.
15. View Work Queue status.
16. View audit history.
17. Understand TeamMate access.
18. Pause or disconnect TeamMate.
19. Receive a visible estimate of work/value delivered.

# 21. Product-Market Fit Question

The first phase of TeamMates exists to answer:

> Will SMEs repeatedly pay for a digital colleague they trust to perform meaningful everyday work?

The product roadmap must remain evidence-led until this is proven.

# 22. Related Documents

- [TMOS Platform Architecture](../architecture/tmos-platform-architecture.md)
- [TeamMate DNA](../architecture/teammate-dna.md)
- [TeamMate Interaction Model](../architecture/teammate-interaction-model.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Admin TeamMate Onboarding and Probation](../product/admin-teammate-onboarding-probation.md)
- [Admin TeamMate UX/UI Specification](../ux/admin-teammate-ux-ui-specification.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
- [Engineering Release Plan](../engineering/engineering-release-plan.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)
