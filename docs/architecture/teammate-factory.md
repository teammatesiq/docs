---
Document title: TeamMate Factory Specification
Version: 1.0
Status: Draft
Owner: TeamMates
Last updated: 2026-08-08
---

# 1. Purpose

This document defines the TeamMate Factory: the TMOS capability used to define, assemble, validate, version and deploy TeamMates.

The Factory exists to ensure that new TeamMate roles are created from governed, reusable platform components rather than implemented as independent AI applications.

The long-term objective is:

> Build TMOS once. Configure many TeamMates.

The Factory is initially an internal product and engineering capability.

It is not part of the Admin TeamMate SME MVP customer experience.

# 2. Architectural Position

A TeamMate is assembled from reusable TMOS components.

Conceptually:

TMOS

↓

TeamMate DNA

↓

Role Definition

↓

Skills

↓

Workflow Catalogue

↓

Default Permissions

↓

Policy Requirements

↓

Knowledge Requirements

↓

Prompt and Reasoning Assets

↓

Interaction Configuration

↓

Validation

↓

Versioned TeamMate Blueprint

↓

Customer Configuration

↓

Deployed TeamMate Instance

The Factory governs the process between role definition and deployable TeamMate.

# 3. Core Principle

A new TeamMate should not require a new platform.

For example:

Admin TeamMate

Project TeamMate

Finance TeamMate

Sales TeamMate

should share common capabilities such as:

- identity
- memory
- permissions
- policy
- approvals
- knowledge retrieval
- audit
- notifications
- workflow orchestration
- AI reasoning
- integrations

Role-specific capability is added through configuration and specialist components.

# 4. Factory Objectives

The TeamMate Factory should:

1. Ensure every TeamMate inherits TeamMate DNA.
2. Standardise TeamMate role definition.
3. Maximise reuse of existing Skills.
4. Maximise reuse of existing Workflows.
5. Ensure permissions are explicit.
6. Ensure governance requirements are defined.
7. Ensure role boundaries are testable.
8. Ensure every TeamMate is versioned.
9. Prevent incomplete or unsafe TeamMates from deployment.
10. Reduce the cost and time required to create future TeamMate roles.

# 5. Factory Non-Objectives

The Factory is not initially:

- a public marketplace
- a no-code AI agent builder
- an unrestricted customer workflow builder
- a prompt playground
- a mechanism for bypassing TeamMate DNA
- a way for customers to create arbitrary autonomous agents

These may represent future opportunities, but they are not part of the initial platform requirement.

# 6. TeamMate Blueprint

The primary output of the Factory is a TeamMate Blueprint.

A Blueprint defines a TeamMate role in a version-controlled form.

Every Blueprint contains:

- identity
- purpose
- role definition
- responsibilities
- boundaries
- success measures
- DNA version
- Skills
- Workflows
- permissions
- policy requirements
- knowledge requirements
- memory rules
- prompts/reasoning assets
- interaction profile
- escalation rules
- evaluation requirements
- deployment configuration

# 7. Blueprint vs Instance

A Blueprint is not a deployed TeamMate.

Example:

Admin TeamMate v1.0

is a Blueprint.

Alex at Acme Ltd

is a deployed TeamMate instance based on that Blueprint.

Multiple organisations may deploy instances of the same Blueprint.

Customer-specific configuration belongs to the instance, not the canonical role definition.

# 8. Identity Definition

Every TeamMate Blueprint defines:

- role key
- role name
- description
- department/category
- purpose
- default display title
- version
- status

Example:

Role Key:

ADMIN_TEAMMATE

Role Name:

Admin TeamMate

Purpose:

Reduce repetitive administrative workload while maintaining human control over external actions.

Customer-selected TeamMate names such as "Alex" belong to deployed instances.

# 9. Role Definition

Every role must explicitly define:

## Purpose

Why the TeamMate exists.

## Responsibilities

Work the TeamMate is expected to perform.

## Boundaries

Work the TeamMate must not perform.

## Outcomes

What successful work looks like.

## Escalation

When human or specialist intervention is required.

No role may be released with undefined boundaries.

# 10. DNA Application

Every TeamMate Blueprint references an approved TeamMate DNA version.

DNA application is mandatory.

The Factory must prevent role configuration from overriding protected DNA behaviours.

Examples include:

- no self-granting permissions
- no silent approval bypass
- no fabricated evidence
- respect for tenant boundaries
- traceability requirements

# 11. Skill Catalogue

The Factory selects capabilities from the TMOS Skill Catalogue.

Example Skills:

- email.read
- email.classify
- email.draft
- email.send
- calendar.read
- calendar.create
- knowledge.search
- meeting.prepare
- meeting.actions.extract
- document.generate
- task.track

Skills are reusable.

They should not be duplicated for individual TeamMate roles unless role-specific behaviour genuinely requires a specialised Skill.

# 12. Skill Definition

Every Skill should define:

- skill key
- name
- purpose
- version
- inputs
- outputs
- required permissions
- failure behaviour
- audit requirements
- supported providers/integrations
- evaluation criteria

Skills should be independently testable where practical.

# 13. Role-to-Skill Mapping

A Blueprint defines which Skills are:

## Required

The role cannot operate without them.

## Optional

May be enabled depending on customer configuration.

## Restricted

Explicitly unavailable to the role.

Example:

Admin TeamMate:

email.draft — Required

knowledge.search — Required

calendar.read — Required

payment.execute — Restricted

# 14. Workflow Catalogue

Each Blueprint references approved workflows.

Example Admin TeamMate workflows:

- Morning Briefing
- Important Email
- Meeting Preparation
- Meeting Follow-Up
- Overdue Action
- Document Request

Workflow definitions remain versioned independently from the TeamMate Blueprint.

This allows workflow improvements without redefining the entire role.

# 15. Workflow Requirements

Each workflow attached to a role must define:

- trigger
- objective
- states
- required Skills
- required permissions
- policy checks
- approval points
- failure behaviour
- escalation
- outputs
- audit requirements
- value measurement

A workflow cannot assume permissions simply because the role contains the relevant Skill.

# 16. Permission Template

Every Blueprint defines default permission requirements.

Permissions should be classified as:

## Required Read

Necessary for core role operation.

## Optional Read

Enables additional capability.

## Prepare

Allows work to be created without external execution.

## Approval-Controlled Execute

May execute following explicit policy/approval.

## Restricted

Unavailable to the role.

Customer deployment may reduce permissions.

Customer configuration must not exceed platform or role restrictions without a separately governed product capability.

# 17. Policy Requirements

A Blueprint may define mandatory policy expectations.

Example:

Admin TeamMate:

External email send requires approval during MVP.

Role policies supplement but do not weaken:

- platform policy
- organisation policy
- security policy
- TeamMate DNA

The most restrictive applicable rule should generally prevail unless an explicitly designed policy-resolution mechanism states otherwise.

# 18. Knowledge Requirements

Every role defines the types of organisational knowledge it may require.

Admin TeamMate examples:

- selected email
- calendar
- approved company documents
- templates
- procedures

Project TeamMate examples might include:

- project plans
- RAID
- governance documents
- status reports
- decisions

The Blueprint defines knowledge requirements.

The customer controls actual authorised sources.

# 19. Memory Profile

Every role defines permitted memory categories.

Examples:

- organisation context
- role-specific memory
- working memory
- personalisation

The role may define:

- expected memory scope
- retention expectations
- sensitivity
- confirmation requirements

Role memory configuration cannot weaken TMOS memory governance.

# 20. Prompt and Reasoning Assets

Prompts are managed implementation assets.

They should not be treated as the TeamMate itself.

Every managed prompt should have:

- identifier
- purpose
- version
- owner
- expected inputs
- expected structured output
- evaluation suite
- release status

Prompts should be replaceable without changing the conceptual role definition.

# 21. Prompt Hierarchy

Prompt assembly should respect the behavioural authority hierarchy.

Conceptually:

Platform Safety

↓

TeamMate DNA

↓

Role

↓

Policy

↓

Workflow

↓

Customer Context

↓

Confirmed Preferences

↓

Current Task

↓

Retrieved Evidence

External retrieved content must not be allowed to redefine higher-level instructions.

# 22. Interaction Profile

Every role may define role-specific interaction defaults.

Examples:

- preferred terminology
- level of detail
- common communication modes
- default recommendation format
- role-specific escalation language

These remain subordinate to TeamMate DNA.

# 23. Evaluation Profile

Every TeamMate Blueprint must define how the role will be tested.

Evaluation areas should include:

- role correctness
- evidence grounding
- permission adherence
- policy adherence
- escalation behaviour
- safe failure
- role-boundary compliance
- workflow quality
- customer usefulness

Role-specific evaluation is mandatory before release.

# 24. Factory Assembly Stages

The Factory lifecycle consists of:

1. Define Role
2. Apply DNA
3. Select Skills
4. Attach Workflows
5. Define Permission Template
6. Define Policy Requirements
7. Define Knowledge Profile
8. Define Memory Profile
9. Attach Reasoning Assets
10. Define Interaction Profile
11. Define Evaluation Profile
12. Validate
13. Version
14. Release Blueprint
15. Deploy Customer Instance

# 25. Stage 1 — Define Role

Required inputs:

- role key
- role name
- purpose
- responsibilities
- boundaries
- success outcomes
- escalation conditions

Output:

Draft Role Definition.

# 26. Stage 2 — Apply DNA

The role selects the current approved DNA version unless a controlled compatibility reason requires another supported version.

Validation ensures:

- protected principles remain intact
- no conflicting role behaviour exists

# 27. Stage 3 — Select Skills

The product owner selects required and optional Skills.

The Factory should identify:

- missing dependencies
- duplicate capabilities
- unsupported combinations
- restricted Skills

# 28. Stage 4 — Attach Workflows

Approved workflow definitions are associated with the role.

Validation checks:

- Skill dependencies
- permission dependencies
- workflow compatibility
- role relevance

# 29. Stage 5 — Permission Template

Define the minimum permissions required to operate the role.

The Factory should flag:

- excessive permissions
- unused permissions
- missing permissions
- prohibited permissions

Least privilege is the default.

# 30. Stage 6 — Policy Requirements

Define mandatory role-level governance.

Example:

A future Finance TeamMate may require stronger approval controls for financial actions than Admin TeamMate requires for document preparation.

# 31. Stage 7 — Knowledge Profile

Define:

- required source types
- optional source types
- restricted information
- expected classification handling

The Blueprint does not grant actual access.

Access occurs only during customer deployment.

# 32. Stage 8 — Memory Profile

Define what the TeamMate may remember and under what conditions.

The Factory should prevent role configuration that attempts to create unrestricted persistent memory.

# 33. Stage 9 — Reasoning Assets

Attach:

- prompts
- structured-output schemas
- tool definitions
- model-routing requirements
- validation logic

These assets must be versioned.

# 34. Stage 10 — Interaction Profile

Define role-specific presentation and communication behaviour.

Examples:

Admin TeamMate may prioritise:

- concise task summaries
- quick approvals
- daily briefing

Project TeamMate may prioritise:

- delivery confidence
- risk
- milestones
- decisions

# 35. Stage 11 — Evaluation Profile

Attach:

- golden datasets
- workflow test cases
- safety tests
- role-boundary tests
- regression thresholds

No Blueprint may progress to release without an evaluation profile.

# 36. Validation

The Factory validates the complete Blueprint.

Validation categories:

## Structural

Required components exist.

## Behavioural

No conflict with TeamMate DNA.

## Permission

Least-privilege model is coherent.

## Workflow

Dependencies are satisfied.

## Governance

Required policies and approvals exist.

## Security

No prohibited access pattern exists.

## Evaluation

Required test coverage exists.

# 37. Validation Failure

A Blueprint that fails validation cannot be released.

The Factory should return actionable findings.

Example:

> Workflow `customer-refund` requires `payment.execute`, which is restricted for Admin TeamMate.

Validation should fail rather than silently modify the role.

# 38. Blueprint Status

Recommended lifecycle:

Draft

→ In Review

→ Validated

→ Released

→ Deprecated

→ Retired

Only Released Blueprints may be deployed to production customers.

# 39. Versioning

TeamMate Blueprints use semantic versioning.

Example:

Admin TeamMate 1.2.0

Recommended interpretation:

MAJOR

Material role or behavioural compatibility change.

MINOR

Backward-compatible capability addition.

PATCH

Backward-compatible correction.

Exact release policy should be formalised as the platform matures.

# 40. Component Version Independence

Blueprint components remain independently versioned.

A deployed TeamMate may reference:

- Blueprint 1.2
- DNA 1.0
- Important Email Workflow 1.4
- Email Draft Skill 2.1
- Prompt 3.2

This enables precise traceability.

# 41. Immutable Released Versions

Released Blueprint versions should not be silently overwritten.

Changes produce a new version.

This ensures customer behaviour can be reconstructed and compared over time.

# 42. Customer Deployment

When a customer hires a TeamMate, TMOS creates a deployed instance from an approved Blueprint.

Deployment adds:

- organisation
- workspace
- customer-selected name
- authorised integrations
- actual permissions
- knowledge sources
- preferences
- probation state

The Blueprint remains unchanged.

# 43. Customer Configuration

Customer configuration may:

- reduce access
- select knowledge
- set working preferences
- configure notifications
- configure permitted options
- personalise communication

It may not:

- override protected DNA
- exceed role restrictions
- disable mandatory audit
- bypass protected security controls

# 44. Probation Deployment

New customer instances initially enter Probation where required by the product.

The Factory defines whether a role supports or requires probation.

For Admin TeamMate MVP:

Probation is mandatory.

# 45. Upgrade Model

A deployed TeamMate should not necessarily receive every new Blueprint version immediately.

Future upgrade model should support:

- compatibility validation
- staged rollout
- customer cohort rollout
- rollback
- feature flags
- evaluation before migration

This prevents platform improvements from creating uncontrolled customer behaviour changes.

# 46. Rollback

The platform should be capable of reverting:

- Blueprint version
- workflow version
- Skill version
- prompt version

where technically feasible.

Rollback requirements are particularly important for AI behaviour changes.

# 47. Factory Audit

Factory activity should be traceable.

Examples:

- Blueprint created
- Skill added
- permission changed
- workflow upgraded
- validation passed
- release approved
- version deployed
- version deprecated

This becomes increasingly important as the TeamMate catalogue grows.

# 48. Factory Roles

Future internal Factory governance may include:

## Product Owner

Defines role outcomes.

## Domain Owner

Validates specialist role behaviour.

## Engineering

Validates implementation.

## Security/Governance

Validates access and controls.

## AI Quality

Validates reasoning behaviour.

One person may perform multiple roles during the MVP stage.

The responsibilities should nevertheless remain conceptually explicit.

# 49. Role Creation Rule

Before creating a new Skill for a TeamMate, ask:

> Can this capability be provided by an existing reusable Skill?

Before creating a new workflow, ask:

> Can an existing workflow be configured or composed?

Before modifying TMOS, ask:

> Is this genuinely a platform requirement or only a role-specific requirement?

This protects the platform from unnecessary complexity.

# 50. Second TeamMate Test

The architecture of the Factory should be validated when the second TeamMate role is created.

If building the second TeamMate requires duplicating:

- identity
- permissions
- memory
- audit
- integrations
- approval infrastructure
- knowledge infrastructure

then the platform abstraction has failed.

# 51. Factory Maturity Model

## Stage 1 — Code-Assisted Factory

Role definitions and components are maintained by Product and Engineering through repository configuration and code.

This is sufficient for Admin TeamMate MVP.

## Stage 2 — Internal Factory UI

Internal tooling allows authorised TeamMates staff to assemble and configure roles.

## Stage 3 — Partner Factory

Selected partners may create specialist roles within strict governance.

## Stage 4 — Ecosystem

Potential governed TeamMate marketplace.

Stages 2–4 are future possibilities, not committed roadmap requirements.

# 52. Marketplace Boundary

A future marketplace must not allow arbitrary code, prompts or agents to bypass TMOS governance.

Marketplace TeamMates would still require:

- DNA compliance
- role definition
- permissions
- validation
- evaluation
- versioning
- governance review

The Factory remains the gatekeeper.

# 53. Relationship to Software Engineering

The Factory does not eliminate software engineering.

New capabilities may still require:

- Skills
- integrations
- workflow primitives
- domain objects
- UI components

The objective is to ensure those capabilities become reusable platform assets rather than being embedded inside one TeamMate.

# 54. Relationship to TMOS

TMOS provides the runtime platform.

The Factory defines what runs on it.

Conceptually:

TMOS = operating environment

TeamMate Factory = role manufacturing system

TeamMate Blueprint = deployable role definition

TeamMate Instance = customer's live digital teammate

# 55. Relationship to TeamMate DNA

DNA defines:

> How every TeamMate must behave.

The Factory defines:

> How a specific TeamMate role is assembled.

A Blueprint cannot redefine DNA.

# 56. Relationship to Customer Experience

SME customers should not need to understand the Factory.

They experience:

Choose TeamMate

↓

Hire

↓

Configure Access

↓

Onboard

↓

Probation

↓

Work

The Factory remains behind that simple experience.

# 57. MVP Factory Scope

For Admin TeamMate MVP, the Factory may be implemented primarily through:

- version-controlled role configuration
- database seed definitions
- workflow definitions
- permission templates
- prompt definitions
- automated validation
- test/evaluation suites

A graphical Factory interface is not required.

# 58. Definition of Done

The Factory foundation is sufficient for Admin TeamMate when:

1. Admin TeamMate has a versioned Blueprint.
2. Blueprint references a DNA version.
3. Responsibilities and boundaries are explicit.
4. Required Skills are defined.
5. Workflows are versioned.
6. Default permissions are explicit.
7. Restricted permissions are explicit.
8. Policy requirements are defined.
9. Knowledge requirements are defined.
10. Memory requirements are defined.
11. Prompt and reasoning assets are versioned.
12. Interaction behaviour is defined.
13. Evaluation coverage exists.
14. Blueprint validation passes.
15. Released versions are immutable.
16. Customer deployment creates a separate TeamMate instance rather than modifying the Blueprint.
17. Customer configuration cannot override protected DNA or security controls.
18. Probation requirements are explicit.
19. Component versions are traceable.
20. The deployed TeamMate can be reconstructed from its recorded Blueprint and component versions.

# 59. Final Factory Principle

The TeamMate Factory exists to prevent TeamMates from becoming a collection of unrelated AI applications.

The long-term architectural objective is:

Build TMOS once. Configure many TeamMates.

A successful Factory means that creating the next TeamMate becomes primarily an exercise in defining:

- role
- skills
- workflows
- permissions
- policy
- knowledge
- memory
- reasoning assets
- evaluation

rather than rebuilding platform capabilities.

If every new TeamMate requires its own:

- identity model
- memory system
- permission system
- audit system
- integration layer
- approval engine

then the platform architecture has failed.

# 60. Related Documents

- [TeamMates Product Requirements Document](../strategy/product-requirements.md)
- [TMOS Platform Architecture](tmos-platform-architecture.md)
- [TeamMate DNA](teammate-dna.md)
- [TMOS Domain Model](tmos-domain-model.md)
- [TeamMate Interaction Model](teammate-interaction-model.md)
- [TMOS System Architecture](tmos-system-architecture.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)
