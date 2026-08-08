---
Document title: TMOS Security, Privacy & Governance Specification
Version: 1.0
Status: Draft
Owner: TeamMates
Last updated: 2026-08-08
---

# 1. Purpose

This document defines the security, privacy, governance and trust model for the TeamMates Operating System (TMOS).

It applies to:

- TMOS
- all TeamMate roles
- all deployed TeamMate instances
- customer integrations
- memory
- knowledge
- workflows
- approvals
- audit
- AI orchestration
- external execution

The objective is to allow TeamMates to perform meaningful business work while maintaining explicit customer control, least privilege, tenant isolation and traceability.

# 2. Security Philosophy

TMOS is designed around the following principles:

1. Least Privilege
2. Explicit Authority
3. Human Accountability
4. Tenant Isolation
5. Defence in Depth
6. Traceability
7. Data Minimisation
8. Safe Failure
9. Transparency
10. Reversibility where practical

Security must be enforced by the platform.

It must not depend solely on AI prompt behaviour.

# 3. Trust Model

Before meaningful work proceeds, TMOS should be able to answer:

- Who is acting?
- For which organisation?
- Which TeamMate is involved?
- What is the requested action?
- Is the action within role?
- Is the action permitted?
- Which policy applies?
- What evidence is being used?
- Is approval required?
- Can the action be traced?

If the system cannot establish sufficient authority or context, controlled execution must stop.

# 4. Governance Hierarchy

Behavioural and governance authority follows this hierarchy:

Platform Safety and Security

↓

TeamMate DNA

↓

Organisation Policy

↓

Workspace Policy

↓

Role Restrictions

↓

Permissions

↓

Workflow Controls

↓

Confirmed Customer Configuration

↓

Current User Instruction

↓

Retrieved Content

Lower layers must never override protected higher layers.

# 5. Governance Layers

TMOS governance operates at multiple levels.

## Platform Governance

Applies universally.

Examples:

- tenant isolation
- authentication requirements
- audit requirements
- prohibited behaviour
- protected security controls

## Organisation Governance

Defined for the customer organisation.

Examples:

- retention
- working policies
- approval requirements
- permitted integrations

## Workspace Governance

Applies to a specific operating area where required.

## Role Governance

Defines role-specific boundaries.

Example:

Admin TeamMate cannot execute payments.

## User Governance

Defines individual authority.

Example:

which user may approve an external action.

## Task Governance

Evaluates the specific action in context.

# 6. Identity Model

Every human user must have a unique TMOS identity.

Relevant attributes include:

- user ID
- organisation
- authentication identity
- workspace membership
- role
- status
- effective permissions

Every deployed TeamMate must also have a unique identity.

Relevant attributes include:

- TeamMate ID
- organisation
- workspace
- role
- Blueprint version
- DNA version
- status
- permission profile
- lifecycle state

No production TeamMate operates anonymously.

# 7. Authentication

Initial supported identity is Microsoft-compatible authentication.

Authentication must use recognised secure identity protocols.

Future support may include:

- Google
- enterprise SSO
- SAML/OIDC providers
- service identities

Where supported, MFA should be encouraged or enforced according to risk and customer identity policy.

# 8. Authentication vs Authorisation

Authentication determines:

> Who are you?

Authorisation determines:

> What are you allowed to do?

Successful authentication must never be treated as unrestricted authority.

# 9. Authorisation

TMOS should enforce authorisation using:

- organisation membership
- workspace membership
- user role
- TeamMate role
- explicit permissions
- resource scope
- applicable policy

Authorisation must be enforced server-side.

Frontend controls are usability features, not security boundaries.

# 10. Least Privilege

Every TeamMate receives only the access necessary for its defined role and approved customer configuration.

Examples:

Admin TeamMate may require:

- email.read
- email.draft
- calendar.read
- selected knowledge.read

It does not require:

- payment.execute
- security.modify
- unrestricted document access

Unused permissions should not be requested merely because they may be useful later.

# 11. Permission Model

Permissions should define:

- action
- resource type
- scope
- decision
- approval requirement
- granting authority
- expiry where relevant

Example:

Permission:

`email.send`

Scope:

approved mailbox

Decision:

Allow

Approval Required:

Yes

# 12. Permission Decisions

Supported decisions include:

## Allow

Action may proceed subject to applicable policy.

## Deny

Action is prohibited.

## Approval Required

Preparation may proceed but execution pauses for authorised human approval.

Explicit denial takes precedence over broad allow.

# 13. Permission Scope

Permissions should support bounded scope.

Examples:

- specific mailbox
- selected SharePoint library
- selected OneDrive folder
- workspace
- particular integration
- particular action class

The system should avoid organisation-wide unrestricted access where narrower access can satisfy the business need.

# 14. Role Restrictions

TeamMate roles may contain protected restrictions.

Example:

Admin TeamMate MVP:

- payment execution prohibited
- contract acceptance prohibited
- security modification prohibited
- permission granting prohibited

Customer configuration cannot override protected role restrictions through normal settings.

# 15. Policy Engine

Policies evaluate contextual business rules independently of AI reasoning.

A policy evaluation may consider:

- actor
- TeamMate
- action
- resource
- organisation
- workspace
- data classification
- permission state
- approval requirement
- risk
- workflow context

Possible decisions:

- allow
- deny
- approval_required
- escalate

# 16. Policy Precedence

Where multiple applicable rules conflict, the more restrictive control should generally prevail unless an explicitly designed precedence rule applies.

Examples:

A broad permission to draft email does not override a policy preventing use of Restricted information.

A user instruction to send immediately does not override an approval requirement.

# 17. Human Approval

Approvals are first-class governance objects.

Approval is required where policy or permission determines that human authority is necessary.

Examples:

- send external email
- modify meeting
- share document externally
- assign work to another person

Approval is specific to the proposed action.

# 18. Approval Integrity

Approval must not be interpreted as:

- permanent future permission
- approval of unrelated actions
- permission to change governance
- permission to modify security
- permission to expand TeamMate authority

The approved action should remain materially equivalent to the action presented to the human.

# 19. Re-Evaluation Before Execution

After approval, TMOS must re-evaluate:

- permission
- policy
- resource state where necessary

before controlled external execution.

This protects against changes occurring between approval request and execution.

# 20. Data Ownership

Customer business data remains owned or controlled by the customer according to the underlying business relationship and applicable law.

TMOS should act only within authorised access.

TeamMates must not treat customer information as their own information.

# 21. Systems of Record

External business systems remain authoritative for their native records.

Examples:

Outlook remains authoritative for email.

Microsoft Calendar remains authoritative for calendar events.

SharePoint remains authoritative for source documents.

TMOS should store only the information required for:

- work state
- memory
- retrieval
- governance
- approvals
- audit
- product operation

# 22. Data Minimisation

TMOS should avoid copying or retaining customer information merely because it is technically possible.

Store the minimum information necessary to:

- perform authorised work
- provide appropriate memory
- preserve audit
- recover workflow state
- measure product operation

# 23. Data Classification

TMOS should support data classification.

Suggested classes:

- Public
- Internal
- Confidential
- Restricted
- Highly Restricted

Classification should influence:

- retrieval
- display
- TeamMate access
- sharing
- logging
- retention
- AI processing where required

# 24. Knowledge Access

Knowledge retrieval must preserve source access boundaries.

The fact that a document has been:

- extracted
- chunked
- embedded
- indexed

must never broaden who can access it.

Every retrievable unit should retain sufficient metadata to enforce access controls.

# 25. Knowledge Source Governance

For each connected knowledge source, TMOS should know:

- organisation
- source
- owner where relevant
- authorised scope
- classification
- integration
- sync status
- access metadata

Users must be able to disconnect authorised sources.

# 26. Memory Governance

Memory is governed business data.

Memory categories include:

- organisation
- workspace
- TeamMate
- working
- personalisation

Every persistent memory should support appropriate metadata such as:

- source
- scope
- owner
- confidence
- sensitivity
- created date
- retention
- lifecycle state

# 27. Personalisation Governance

Personalisation may include:

- writing preference
- briefing time
- preferred terminology
- priority contacts
- working preferences

Personalisation must not:

- override security
- override policy
- expand permissions
- remove approvals
- create discriminatory protected behaviour
- convert one-off exceptions into broad rules without evidence

# 28. Memory Transparency

Users should be able to understand important persistent personalisation.

Where appropriate, they should be able to:

- view
- confirm
- reject
- amend
- remove

learned preferences.

# 29. Data Retention

Retention should be defined by data type and applicable policy.

Different rules may apply to:

- temporary working context
- personalisation
- conversation history
- knowledge index
- audit
- integration metadata

Retention defaults should not be confused with legal obligations.

# 30. Data Deletion

Deletion requirements should distinguish:

- source disconnection
- deletion of derived retrieval content
- deletion of personalisation
- user deletion
- organisation deletion
- legal/audit retention obligations

A customer should not have to leave an integration connected merely to access account-management functions.

# 31. Encryption

TMOS must use encryption in transit.

Sensitive persisted information must use encryption at rest appropriate to the hosting platform and risk profile.

Protected credentials and secrets require stronger handling than ordinary application content.

# 32. Secrets Management

Do not store raw secrets in ordinary source code or customer-facing configuration.

Use managed secret or credential storage for:

- provider credentials
- encryption material
- service secrets
- OAuth token material where appropriate

Secret access should be restricted to the minimum required runtime components.

# 33. OAuth Governance

Microsoft 365 connection must use the minimum scopes required for current product capabilities.

OAuth consent should be explained to the customer in plain language before or during connection.

TMOS should expose:

- connected identity
- granted capability
- integration health
- ability to disconnect

# 34. Token Handling

Access and refresh tokens must:

- be protected at rest
- never be exposed to frontend clients unnecessarily
- never appear in ordinary logs
- be revoked or rendered unusable after disconnection where supported

# 35. Tenant Isolation

Organisation is the primary tenant boundary.

Tenant isolation applies to:

- users
- TeamMates
- workspaces
- tasks
- workflows
- approvals
- memory
- knowledge
- integrations
- policies
- notifications
- audit

Cross-tenant access is prohibited.

# 36. Defence in Depth for Tenancy

Tenant isolation should be enforced through multiple layers where practical:

- authenticated organisation membership
- application-service checks
- organisation-scoped queries
- database foreign keys
- Row Level Security
- tenant-aware retrieval
- automated isolation tests

No single control should be assumed infallible.

# 37. Workspace Isolation

Where organisations contain multiple Workspaces, access should also respect:

- workspace membership
- TeamMate assignment
- knowledge scope
- workspace policy

A user or TeamMate should not automatically gain access to every workspace because they belong to the organisation.

# 38. AI Provider Boundary

AI providers are reasoning services.

They are not TMOS systems of record.

AI providers do not own:

- customer identity
- permission decisions
- policy decisions
- workflow state
- approvals
- canonical memory
- audit authority

TMOS remains responsible for governance.

# 39. AI Data Minimisation

Reasoning requests should include only the context required for the current task.

Avoid sending unnecessary:

- documents
- mailbox history
- personal information
- unrelated organisational context

to the model provider.

# 40. Prompt Governance

Prompts are governed implementation assets.

Production prompts should be:

- identified
- versioned
- owned
- tested
- released deliberately

Unmanaged production prompts should be avoided.

# 41. Prompt Injection

External content may contain malicious or conflicting instructions.

Sources include:

- email
- documents
- transcripts
- websites
- external applications

Such instructions are untrusted content.

They must not override:

- platform safety
- TeamMate DNA
- policy
- permissions
- workflow authority

# 42. Indirect Prompt Injection Controls

Controls should include:

- strict instruction hierarchy
- provider-independent permission checks
- policy checks outside the model
- structured tool invocation
- output validation
- restricted tool access
- adversarial evaluation

The control model must not rely solely on model compliance.

# 43. Tool and Skill Security

AI reasoning may request execution of a Skill.

It must not directly receive unrestricted external-system authority.

Preferred sequence:

AI requests structured action

↓

TMOS validates action

↓

Permission check

↓

Policy check

↓

Approval where required

↓

Skill executes

↓

Result confirmed

↓

Audit

# 44. AI Output Validation

Model output used to influence workflow or external action should be validated appropriately.

Potential validation includes:

- schema
- required fields
- evidence
- prohibited claims
- role boundary
- action type
- confidence
- policy compatibility

Invalid output must not automatically advance controlled work.

# 45. No Hidden Reasoning Requirement

TMOS should not depend on exposing private model chain-of-thought for customer explainability or audit.

Explainability should use structured data such as:

- evidence
- sources
- rationale
- assumptions
- policy result
- confidence
- resulting action

# 46. Audit

Every meaningful action should produce an audit event where appropriate.

Audit should capture sufficient information to reconstruct:

- who acted
- which TeamMate acted
- what happened
- why
- evidence
- approval
- policy
- permission
- relevant versions
- outcome
- time

# 47. Audit Immutability

Audit events should be append-only through ordinary product operations.

Users and TeamMates must not silently rewrite historical audit records.

Corrections should create additional records rather than erasing history where audit obligations require preservation.

# 48. Audit Access

Customer administrators should be able to inspect meaningful TeamMate activity.

Standard customer audit presentation should use readable business language.

Technical metadata may be available as secondary detail.

# 49. Logging vs Audit

Operational logging and business audit are different.

Logs support:

- diagnosis
- performance
- operational monitoring

Audit supports:

- accountability
- business reconstruction
- governance
- trust

Logs should not be treated as the sole audit mechanism.

# 50. Logging Privacy

Operational logs should avoid unnecessary sensitive content.

Do not routinely log:

- full email bodies
- unrestricted documents
- OAuth tokens
- credentials
- complete prompts containing customer content
- unnecessary personal data

# 51. Safe Failure

When a security or governance check cannot be completed reliably, controlled execution should fail closed.

Examples:

- permission service unavailable
- uncertain tenant context
- missing approval
- authentication invalid
- policy evaluation unavailable for high-risk action

Preparation-only work may continue where it remains safe and clearly separated from execution.

# 52. Integration Failure

If an external integration fails:

- dependent external action should stop
- work state should be preserved
- safe retries may occur
- the customer should be informed when intervention is required

TMOS must not fabricate successful completion.

# 53. Human Override

Authorised humans must be able to:

- reject TeamMate work
- pause TeamMate execution
- revoke permissions
- disconnect integrations
- disable learning
- correct relevant data
- cancel eligible workflows

TeamMates must not resist legitimate governance actions.

# 54. TeamMate Suspension

Suspending a TeamMate should:

- stop new active execution
- stop scheduled TeamMate work where appropriate
- preserve required work state
- preserve audit
- prevent new external actions

Suspension should not silently delete customer data.

# 55. Integration Disconnection

Disconnecting an integration should:

- prevent future access
- stop dependent workflows
- mark integration unavailable
- trigger appropriate token revocation where supported
- schedule cleanup of derived retrievable data according to policy

# 56. Security Monitoring

TMOS should monitor for signals including:

- repeated authentication failure
- repeated authorisation denial
- cross-tenant access attempts
- unexpected permission change
- abnormal external execution attempts
- integration abuse
- suspicious webhook behaviour
- secret/configuration failure

# 57. Security Incident Model

Security incidents should be managed through a defined lifecycle.

Suggested stages:

Detect

↓

Assess

↓

Contain

↓

Investigate

↓

Recover

↓

Review

Meaningful incidents should have:

- incident identifier
- severity
- timeline
- affected organisations
- impact
- containment
- root cause
- corrective action

# 58. Security Severity

Examples:

## Critical

- confirmed cross-tenant data exposure
- uncontrolled material external action
- credential compromise with active exploitation

## High

- exploitable authorisation flaw
- sensitive-data exposure
- significant permission-control failure

## Medium

- restricted but lower-impact control weakness

## Low

- minor security defect with limited practical impact

Severity methodology should mature with the platform.

# 59. Customer Trust Centre

The product should provide a Trust & Governance experience showing relevant items such as:

- active TeamMates
- connected systems
- permissions
- knowledge sources
- pending approvals
- audit activity
- learning
- data controls
- integration health

Governance should be visible rather than hidden behind technical configuration.

# 60. Permission Transparency

Customers should be able to understand TeamMate authority in plain language.

Example:

Read email — Allowed

Draft email — Allowed

Send external email — Approval required

Read selected documents — Allowed

Delete documents — Not allowed

Make payments — Not allowed

# 61. Approval Transparency

The customer should be able to inspect:

- pending approvals
- approved actions
- rejected actions
- who made the decision
- what was approved
- resulting execution

# 62. Knowledge Transparency

Customers should be able to see:

- connected knowledge sources
- access scope
- last sync
- connection health
- ability to disconnect

# 63. Privacy Rights Support

TMOS should be designed to support applicable customer and data-subject rights where required.

Potential capabilities include:

- access
- export
- correction
- deletion
- restriction

Exact obligations depend on legal role, geography and data type.

# 64. Regulatory Position

The initial product should be designed with UK and European privacy expectations in mind.

Relevant frameworks may include:

- UK GDPR
- EU GDPR

Future security assurance objectives may include:

- Cyber Essentials
- Cyber Essentials Plus
- ISO 27001
- SOC 2

These are maturity objectives unless explicitly achieved and certified.

Do not claim certification or formal compliance without evidence.

# 65. Data Processing Documentation

As the product matures, TeamMates should maintain appropriate documentation covering:

- categories of processed data
- processing purpose
- subprocessors
- retention
- security controls
- customer responsibilities
- international transfer arrangements where relevant

# 66. Subprocessor Governance

Third-party providers that process customer information should be subject to appropriate review.

Examples may include:

- cloud hosting
- AI providers
- authentication providers
- monitoring providers
- billing provider where applicable

Maintain a controlled record of relevant subprocessors.

# 67. AI Provider Governance

AI provider adoption should consider:

- data handling
- retention behaviour
- contractual terms
- geographic processing
- security controls
- model capability
- reliability

Provider choice is an architecture and governance decision, not merely a quality decision.

# 68. Support Access

Internal support personnel should not automatically have unrestricted access to customer business content.

Support tooling should prefer:

- configuration
- status
- health
- error metadata
- workflow state

Content access, if ever necessary, should be:

- justified
- scoped
- controlled
- auditable

# 69. Development and Test Data

Production customer information should not routinely be copied into development or test.

Testing should prefer:

- synthetic data
- dedicated test tenants
- sanitised examples

Any exceptional production-data use for diagnosis should be governed.

# 70. Secure Development

The engineering lifecycle should include:

- dependency scanning
- secret scanning
- code review
- automated testing
- security testing
- access-control testing
- migration testing
- AI safety evaluation

# 71. Threat Modelling

Threat modelling should be performed for material features and integration changes.

Initial focus areas include:

- tenant isolation
- Microsoft OAuth
- email execution
- document retrieval
- AI tool invocation
- prompt injection
- knowledge access
- support tooling
- billing webhooks

# 72. Security Testing

Before controlled external beta, testing should include:

- authentication
- authorisation
- tenant isolation
- permission enforcement
- RLS
- session security
- input validation
- webhook validation
- prompt injection
- indirect prompt injection
- duplicate external execution
- secrets handling

# 73. Security Release Gate

The product must not enter controlled external beta with:

- unresolved critical security vulnerabilities
- known cross-tenant access defects
- known approval bypass
- known uncontrolled external execution
- exposed production secrets

High-severity findings require explicit resolution or formal risk decision before release.

# 74. Governance Release Gate

Before beta:

- Admin TeamMate role boundaries are defined.
- Permission profile is explicit.
- Restricted actions are enforced.
- Approval workflow is proven.
- Audit is operational.
- Customer can pause TeamMate.
- Customer can disconnect integrations.
- Knowledge scope is visible.
- Probation is operational.

# 75. Privacy Release Gate

Before beta:

- data flows are understood
- required customer permissions are explicit
- retention defaults are documented
- deletion/disconnection behaviour is defined
- sensitive logging is controlled
- production/test separation exists
- third-party providers are identified

# 76. TeamMate Trust Requirements

A customer should be able to answer:

> What can my TeamMate see?

> What can my TeamMate do?

> What must I approve?

> What has it done?

> What has it learned?

> Where did this answer come from?

> How do I stop it?

If the product cannot answer these clearly, the trust model is incomplete.

# 77. Security Anti-Patterns

Do not:

- rely on hidden prompts as permission controls
- give AI unrestricted tool access
- use frontend-only authorisation
- share credentials between tenants
- put sensitive customer data into general logs
- silently broaden OAuth scopes
- automatically grant new permissions after probation
- treat embeddings as outside access control
- treat customer approval as unlimited delegation
- claim compliance certification without certification

# 78. Future Enterprise Controls

Potential future enterprise capabilities include:

- SAML/OIDC enterprise SSO
- SCIM
- customer-managed encryption keys
- advanced ABAC
- data residency controls
- dedicated deployment
- customer-managed cloud deployment
- security analytics
- policy simulation
- enhanced DLP integration
- SIEM integration

These are not SME MVP requirements.

# 79. Security Architecture Principle

The safest place to enforce governance is outside the model.

AI can:

- understand
- classify
- recommend
- prepare

TMOS decides:

- whether access is allowed
- whether execution is permitted
- whether approval is required
- whether an action proceeds

This separation is fundamental.

# 80. Definition of Done

The security, privacy and governance model is sufficiently implemented for controlled beta when:

1. Users authenticate securely.
2. Tenant isolation is proven.
3. Permissions are enforced server-side.
4. Restricted role actions are blocked.
5. Policies are enforced independently of AI.
6. External controlled actions require approval.
7. Approval is revalidated before execution.
8. OAuth credentials are appropriately protected.
9. Integration disconnection prevents future access.
10. Knowledge retrieval preserves source boundaries.
11. Memory is scoped and governed.
12. Significant actions are auditable.
13. Audit cannot be silently rewritten.
14. Sensitive data is minimised in logs.
15. Prompt-injection controls are tested.
16. Duplicate external execution is prevented.
17. Customer can pause Admin TeamMate.
18. Customer can review permissions.
19. Customer can review connected knowledge.
20. Security monitoring exists for major trust failures.

# 81. Final Governance Principle

The goal is not maximum autonomy.

The goal is maximum useful delegation within explicit, understandable authority.

The defining principle is:

> Trust before autonomy.

A TeamMate earns broader responsibility through reliable, transparent behaviour.

It never grants that responsibility to itself.

# 82. Related Documents

- [TeamMates Product Requirements Document](../strategy/product-requirements.md)
- [TMOS Platform Architecture](../architecture/tmos-platform-architecture.md)
- [TeamMate DNA](../architecture/teammate-dna.md)
- [TeamMate Factory](../architecture/teammate-factory.md)
- [TMOS Domain Model](../architecture/tmos-domain-model.md)
- [TeamMate Interaction Model](../architecture/teammate-interaction-model.md)
- [TMOS System Architecture](../architecture/tmos-system-architecture.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)
