---
Document title: TMOS Platform Architecture
Version: 1.0
Status: Draft
Owner: TeamMates
Last updated: 2026-08-08
---

# 1. Purpose

This document defines the logical architecture of the TeamMates Operating System (TMOS).

TMOS is the shared platform that provides the capabilities required by every TeamMate.

Individual TeamMates are role-specific digital colleagues that run on TMOS.

This document defines the platform architecture, component boundaries, runtime model, governance model, extensibility principles and deployment philosophy.

# 2. Architectural Position

The TeamMate belongs to TeamMates.

It does not belong to Microsoft Teams, Outlook, Copilot, Slack or any other interaction surface.

These external products are channels and systems through which a TeamMate may work.

The TeamMate identity, permissions, memory, governance, lifecycle and runtime remain controlled by TMOS.

# 3. Platform Vision

TMOS is the operating system for governed digital colleagues.

It provides the shared capabilities required to create, deploy, manage and govern TeamMates consistently.

TMOS is not itself the primary SME customer proposition.

Customers primarily buy TeamMates.

TMOS is the platform that makes those TeamMates reliable, governed and scalable.

# 4. Core Architecture Principles

TMOS shall:

1. Separate digital employee identity from interaction channels.
2. Keep humans accountable for important decisions.
3. Treat permissions and policies as first-class platform capabilities.
4. Preserve traceability across all meaningful work.
5. Keep organisational data tenant-isolated.
6. Allow TeamMate roles to reuse common capabilities.
7. Remain independent of any single AI model provider.
8. Remain independent of any single productivity ecosystem.
9. Support event-driven work rather than chat-only interaction.
10. Optimise the SME MVP for simplicity rather than premature infrastructure complexity.

# 5. High-Level Architecture

Conceptually:

Experience Layer

- TeamMates Web App
- Microsoft Teams
- Outlook
- Future Slack
- Future Mobile
- Future Copilot surfaces

↓

TMOS Control and Runtime Layer

- Identity
- Organisation and Workspace
- TeamMate Runtime
- Role
- Skills
- Workflow
- Policy
- Permissions
- Approval
- Memory
- Knowledge
- Notification
- Audit
- Integration
- Billing
- Administration

↓

AI and Reasoning Layer

- Model orchestration
- Prompt management
- Tool invocation
- Response validation
- Confidence handling
- Provider abstraction

↓

Connector Layer

- Microsoft 365
- Future Google Workspace
- Future CRM
- Future finance systems
- Future collaboration tools

↓

Customer Systems of Record

- Outlook
- Calendar
- SharePoint
- OneDrive
- Other approved business systems

# 6. Experience Plane

The Experience Plane contains the user-facing surfaces through which humans interact with TeamMates.

Initial surface:

- TeamMates web application

Priority external surface:

- Microsoft Teams

Other potential surfaces:

- Outlook
- Slack
- browser extensions
- mobile applications
- Copilot

The Experience Plane shall not own core TeamMate business logic.

It consumes TMOS services.

# 7. Control Plane

The TMOS Control Plane manages:

- organisations
- workspaces
- users
- TeamMate deployment
- role configuration
- permissions
- policies
- integrations
- billing
- audit
- governance
- lifecycle state
- administration

The Control Plane defines what a TeamMate is allowed to do and how it is configured.

# 8. Runtime Plane

The TeamMate Runtime executes work.

Each deployed TeamMate has an independent runtime identity and state.

The runtime coordinates:

- Role
- TeamMate DNA
- Skills
- Workflow state
- Memory
- Knowledge
- Policy
- Permissions
- Reasoning
- Approvals
- External actions
- Audit

The runtime must not bypass TMOS governance services.

# 9. TeamMate Composition Model

Every deployed TeamMate is assembled from:

TMOS

↓

TeamMate DNA

↓

Role Definition

↓

Skills

↓

Permissions

↓

Policies

↓

Workflows

↓

Knowledge

↓

Memory

↓

Customer Configuration

↓

Live Runtime

This composition model allows future TeamMate roles to reuse the same platform foundation.

# 10. TeamMate DNA

Every TeamMate inherits the shared TeamMate DNA specification.

TeamMate DNA defines platform-wide behavioural principles including:

- honesty
- transparency
- human control
- professional behaviour
- safe learning
- escalation
- collaboration
- evidence use

Role configuration may specialise behaviour but must not override protected DNA principles.

# 11. Role Model

A Role defines what type of digital colleague a TeamMate is.

Examples:

- Admin TeamMate
- Project TeamMate
- Finance TeamMate
- Sales TeamMate
- Marketing TeamMate
- HR TeamMate

A Role defines:

- purpose
- responsibilities
- success measures
- default skills
- default permissions
- workflow catalogue
- escalation boundaries

The Role is separate from the deployed TeamMate instance.

# 12. Skills Model

Skills are reusable platform capabilities.

Examples:

- read email
- draft email
- search knowledge
- read calendar
- prepare meeting
- extract actions
- generate document
- summarise content

Roles select and configure Skills.

Skills should be versioned and reusable.

A new TeamMate should not require rewriting common capabilities.

# 13. Workflow Model

Workflows coordinate meaningful business work.

Examples:

- Important Email
- Morning Briefing
- Meeting Preparation
- Meeting Follow-Up
- Overdue Action
- Document Request

Workflow responsibilities include:

- trigger handling
- state
- dependencies
- retries
- approval waits
- escalation
- completion
- cancellation

TMOS should support event-driven workflow execution.

# 14. Event-Driven Model

TeamMates do not operate only when a user opens chat.

They respond to approved events.

Examples:

- EmailReceived
- MeetingUpcoming
- MeetingCompleted
- TaskCreated
- ApprovalGranted
- KnowledgeUpdated
- PolicyChanged
- IntegrationDisconnected

Events allow TeamMates to perform proactive work while remaining governed.

# 15. Permission Model

Permissions are explicit platform objects.

Examples:

- email.read
- email.draft
- email.send
- calendar.read
- calendar.create
- document.read
- document.share

Permissions shall define:

- action
- resource
- scope
- owner
- approval requirement
- expiry where relevant

Absence of permission means denial.

Least privilege is mandatory.

# 16. Policy Model

Policies govern whether actions are allowed in a specific organisational context.

Examples:

- external email requires approval
- restricted documents cannot be used by a specific role
- working-hours rules
- approval thresholds
- retention rules

Policy evaluation occurs independently of AI reasoning.

Policies override:

- prompts
- workflow suggestions
- learned preferences
- role-level recommendations

# 17. Approval Model

Approvals are first-class platform objects.

Approval classes:

## Inform

No decision required.

## Prepare

Work can be prepared without execution.

## Approval Required

Explicit human approval required before external execution.

## Restricted

Action prohibited.

For MVP, important external actions remain approval-controlled.

# 18. Memory Architecture

TMOS maintains governed memory.

Memory categories:

## Organisation Memory

Shared organisational context.

Examples:

- company terminology
- structure
- standard processes

## Workspace Memory

Context specific to a team or operational area.

## TeamMate Memory

Role-specific persistent context.

## Working Memory

Short-lived context for active work.

## Personalisation Memory

Confirmed user preferences.

Every memory item should have:

- source
- owner
- confidence
- scope
- sensitivity
- retention
- lifecycle

Memory may not silently override permissions or governance.

# 19. Knowledge Architecture

Knowledge represents approved organisational information connected to TMOS.

Potential sources:

- SharePoint
- OneDrive
- Google Drive
- uploaded files
- policies
- procedures
- meeting records

Knowledge retrieval must preserve source permissions.

TMOS should favour connection to systems of record rather than unnecessary copying of entire business systems.

# 20. AI Orchestration

AI provides reasoning within TMOS.

The AI orchestration capability is responsible for:

- prompt assembly
- context retrieval
- model selection
- structured outputs
- tool invocation
- output validation
- confidence handling
- fallback behaviour

AI models do not own:

- permissions
- policies
- audit
- customer identity
- workflow authority
- system-of-record data

# 21. Provider Independence

TMOS shall abstract model-provider integration.

Initial provider may be OpenAI.

Future providers may include:

- Azure OpenAI
- other specialist models

Provider selection may depend on:

- quality
- latency
- cost
- customer requirement
- geography
- compliance

Core product behaviour must not require a redesign when changing model provider.

# 22. Integration Architecture

External systems are accessed through a standard Integration Layer.

The platform should expose provider-independent capabilities internally.

For example:

- mail.list
- mail.get
- mail.draft
- mail.send
- calendar.list
- calendar.create
- files.search
- files.get

Microsoft Graph is one implementation of these capabilities.

This prevents provider-specific logic from spreading throughout TMOS.

# 23. Microsoft 365 Strategy

Microsoft 365 is the priority SME ecosystem for the first release.

Initial integration scope includes:

- Outlook email
- Calendar
- Contacts where needed
- SharePoint
- OneDrive

Microsoft Teams should become an important future interaction surface.

TMOS remains the control plane.

Microsoft 365 remains the source of record for its native business data.

# 24. Multi-Tenancy

TMOS is multi-tenant.

Every organisation has an isolated tenant boundary.

Isolation applies to:

- users
- TeamMates
- memory
- knowledge
- documents
- tasks
- approvals
- policies
- audit
- integrations

Cross-tenant access is prohibited.

Tenant boundaries must be enforced at application and data layers.

# 25. Workspace Model

An Organisation may contain one or more Workspaces.

A Workspace groups:

- users
- TeamMates
- workflows
- knowledge
- policies
- tasks

For the SME MVP, a single default workspace may be created automatically.

The model remains extensible for future larger customers.

# 26. Security Architecture

TMOS follows:

- least privilege
- zero-trust assumptions
- encrypted data in transit
- encrypted data at rest
- secure secret storage
- explicit permissions
- auditability
- tenant isolation

Security controls must exist in the platform layer rather than relying on TeamMate prompt behaviour.

# 27. Audit Architecture

Every meaningful action should produce traceability.

Audit should capture:

- actor
- organisation
- TeamMate
- action
- reason
- evidence
- policy decision
- approval
- outcome
- relevant versions
- timestamp

Audit is append-only.

# 28. Observability

TMOS shall provide operational visibility into:

- API health
- workflow state
- integration health
- queue health
- AI execution
- failures
- latency
- retry behaviour
- cost metadata
- security events

Operational telemetry should minimise exposure of sensitive customer content.

# 29. SME MVP Physical Architecture

The logical architecture defines clear service boundaries.

The MVP should not immediately deploy every logical component as an independent microservice.

Recommended first implementation:

- modular backend application
- PostgreSQL
- pgvector
- managed object storage
- managed queue/background workers
- Microsoft Graph integration
- OpenAI integration
- Stripe
- web frontend

Logical boundaries should be preserved in code so services can be separated later where justified.

# 30. Modular Monolith Decision

For the SME MVP, prefer a modular monolith over premature microservices.

Reasons:

- faster delivery
- simpler deployment
- lower operational overhead
- simpler debugging
- easier transaction management
- smaller engineering team

This is not a rejection of service-oriented architecture.

It is a deployment decision for the first stage.

# 31. Data Architecture

PostgreSQL is the primary transactional store.

Recommended MVP storage:

- PostgreSQL for business objects
- pgvector for semantic retrieval
- object storage for files
- queue infrastructure for asynchronous jobs

Avoid introducing multiple specialist databases without demonstrated need.

# 32. Systems of Record

TMOS should not automatically become the system of record for external business data.

Examples:

Outlook remains system of record for email.

Microsoft Calendar remains system of record for calendar events.

SharePoint remains system of record for source documents.

TMOS is authoritative for:

- TeamMate identity
- role state
- permissions
- policies
- workflow state
- approvals
- learning
- audit
- TeamMate configuration

# 33. TeamMate Factory

The TeamMate Factory is the platform capability used to define and deploy TeamMate roles.

It assembles:

- TeamMate DNA
- Role
- Skills
- Permissions
- Workflows
- Prompt library
- Knowledge requirements
- configuration

The long-term goal is for new TeamMate roles to be substantially configuration-driven rather than separate software products.

# 34. TeamMate Lifecycle

A deployed TeamMate lifecycle is exactly (D-001 / F-003):

Configuring

→ Probation

→ Active

→ Suspended

→ Archived

A TeamMate must never automatically gain additional authority merely by becoming Active.

Permissions remain explicit.

Draft may be used by versioned definition and Blueprint lifecycles, but is not a deployed TeamMate lifecycle state.

Customer-facing **Paused** maps to `status = suspended` and `suspension_reason = customer_paused`; it is not a separate domain state. Other supported reasons may include `trial_expired`, `subscription_suspended`, `security_suspension` and `admin_suspended`.

While Suspended, TMOS must block new active execution and new controlled external actions, stop scheduled TeamMate work where appropriate, and preserve durable workflow and task state, configuration, required audit history and customer data according to applicable retention rules.

Reactivation must revalidate relevant subscription or entitlement, integrations, permissions, policy and TeamMate configuration before execution resumes.

# 35. Probation Architecture

Probation is a first-class TeamMate state.

It supports:

- enhanced supervision
- higher approval requirements
- learning validation
- connection health checks
- permission validation
- trust measurement

Probation completion represents operational readiness, not unrestricted autonomy.

# 36. Collaboration Architecture

Future TMOS versions may support structured TeamMate-to-TeamMate hand-offs.

Example:

Sales TeamMate

→ Admin TeamMate

→ Finance TeamMate

→ Project TeamMate

Each TeamMate remains bounded by its role and permissions.

Every hand-off must remain auditable.

Multi-TeamMate orchestration is explicitly outside the first Admin TeamMate MVP.

# 37. Enterprise Evolution

TMOS should be architected so the platform can later support:

- enterprise SSO
- advanced governance
- data residency
- customer-managed deployment
- enhanced audit
- advanced role controls
- Microsoft Copilot integration
- private-cloud deployment where justified

The SME MVP should not implement these capabilities prematurely.

# 38. Deployment Independence

TMOS should support multiple future deployment patterns.

Potential models:

## TeamMates SaaS

Standard hosted model.

Primary SME deployment.

## Enterprise Dedicated

Dedicated or logically enhanced deployment for larger customers.

## Customer-Managed

Potential future customer-controlled cloud deployment.

These are future capabilities rather than MVP requirements.

# 39. Architecture Boundaries

TMOS should not become:

- a generic chatbot builder
- unrestricted agent platform
- general automation builder
- replacement CRM
- replacement productivity suite
- replacement document management system

The platform exists specifically to support governed digital colleagues.

# 40. Architecture Quality Attributes

TMOS should optimise for:

- security
- trust
- reliability
- explainability
- extensibility
- maintainability
- operational simplicity
- provider independence
- tenant isolation
- controlled scalability

# 41. Long-Term Strategic Asset

The strategic asset is not the Admin TeamMate alone.

The strategic asset is the platform that allows TeamMates to be created, governed and deployed repeatedly.

Admin TeamMate validates the platform.

Future TeamMates expand it.

# 42. Core Architectural Principle

The defining architectural principle is:

> The TeamMate lives in TMOS and works through the customer's existing tools.

TMOS owns:

- identity
- permissions
- governance
- memory
- work state
- lifecycle
- traceability

External systems provide:

- interaction surfaces
- source data
- business actions

This separation preserves TeamMates as an independent platform while allowing TeamMates to feel native inside the customer's working environment.

# 43. Related Documents

- [TeamMates Product Requirements Document](../strategy/product-requirements.md)
- [TeamMate DNA](teammate-dna.md)
- [TeamMate Factory](teammate-factory.md)
- [TMOS Domain Model](tmos-domain-model.md)
- [TeamMate Interaction Model](teammate-interaction-model.md)
- [TMOS System Architecture](tmos-system-architecture.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
