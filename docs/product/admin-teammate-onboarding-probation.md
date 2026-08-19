---
Document title: Admin TeamMate Onboarding and Probation
Version: 1.1
Status: Controlled
Owner: Product and Experience Authorities
Last updated: 2026-08-19
---

# 1. Purpose

This document defines how a qualifying customer establishes an organisation, hires and configures Admin TeamMate, connects supported Microsoft 365 sources, understands the trust boundary, enters Probation and progresses to Active status.

Onboarding is not complete when an account is created. It is complete when the correct customer can receive and review useful, governed live-business work and understands what the TeamMate can and cannot do.

# 2. Objectives

Onboarding must:

- establish the correct human and organisation identity;
- make Admin TeamMate’s role clear;
- obtain only the permissions required for the controlled capability;
- explain evidence, review and no-external-effect boundaries;
- configure enough context to deliver first value;
- validate integration and workflow readiness;
- begin in Probation rather than silently granting normal operation;
- give the customer clear pause, disconnect and support routes;
- minimise configuration that is not required for first value.

# 3. Initial customer and owner

The initial customer is normally a UK SME using Microsoft 365.

A named **Organisation Owner** is accountable for:

- creating or selecting the correct TeamMates organisation;
- completing sign-in and membership resolution;
- hiring/configuring Admin TeamMate;
- connecting supported Microsoft sources;
- understanding and granting delegated permissions;
- confirming initial operating preferences and facts;
- reviewing first work;
- deciding whether probation may complete;
- pausing, disconnecting or escalating where necessary.

A Microsoft mailbox or calendar identity does not itself create TeamMates organisation membership.

# 4. Prerequisites

Before controlled onboarding begins:

- the customer falls within the supported launch profile or has an explicit exception;
- an accountable Organisation Owner is identified;
- the customer can sign in through the supported TeamMates identity boundary;
- the owner has appropriate authority to connect the relevant Microsoft account;
- the customer accepts the current delegated read-only permission boundary;
- a supported development, internal-alpha or beta environment is available;
- support and incident routes are defined;
- no known security or entitlement block prevents activation.

For the current internal-alpha boundary, the release and principal-specific feature gates must also be valid.

# 5. Canonical deployed lifecycle

Admin TeamMate follows:

**Configuring → Probation → Active → Suspended → Archived**

There is no deployed Draft state.

## 5.1 Configuring

The TeamMate exists in the customer organisation, but required identity, connection, permission, policy or role configuration is incomplete or being validated.

Normal active workflows must not begin until their prerequisites are verified.

## 5.2 Probation

The TeamMate performs bounded live-business work with heightened explanation, explicit customer review and active readiness checks.

Probation is a trust-building and validation state, not a time-limited free pass to broaden capability.

## 5.3 Active

The customer and platform have confirmed readiness for the approved workflows. Active status does not automatically grant additional provider permissions, external effects or autonomy.

## 5.4 Suspended

No new execution starts. Scheduled work stops where appropriate. No controlled external action executes. Durable state, configuration and required audit history remain preserved.

Customer-facing **Paused** maps to:

- `status = suspended`;
- `suspension_reason = customer_paused`.

Other supported reasons may include trial expiry, subscription suspension, security suspension or administrative suspension.

## 5.5 Archived

The TeamMate no longer operates. Access, retention and deletion follow applicable policy and contractual requirements.

# 6. Onboarding journey

## Step 1 — Welcome and role clarity

The experience introduces Admin TeamMate as a digital colleague with a defined role.

The customer should understand:

- the work Admin TeamMate is intended to help with;
- that it is not a generic chatbot or employee-replacement claim;
- that important work remains visible and reviewable;
- that current Microsoft access is read-only;
- that nothing is sent or changed externally in the controlled release.

Recommended primary action:

**Hire Admin TeamMate**

## Step 2 — Establish TeamMates identity

The customer signs in to TeamMates.

The platform must:

- validate the supported authentication boundary;
- resolve the persisted user identity;
- resolve exactly one eligible organisation membership;
- block unknown, revoked or ambiguous membership;
- avoid disclosing another organisation’s existence or data.

Authentication alone does not grant organisation access.

## Step 3 — Create or select the organisation

Where supported, the owner creates or selects the organisation that will own Admin TeamMate.

Capture only information required for:

- organisation identity;
- billing/entitlement where applicable;
- role and policy configuration;
- first-value workflows;
- support and accountability.

Avoid a long business interview before the customer can see value. Additional context should be requested when required by a real workflow.

## Step 4 — Hire and configure Admin TeamMate

The platform creates the deployed TeamMate in **Configuring**.

Configuration includes at minimum:

- role: Admin TeamMate;
- current role/version identity;
- organisation ownership;
- current lifecycle status;
- approved workflow/feature configuration;
- current permission ceiling;
- communication of current limitations.

Project TeamMate or another role must not appear as an SME v1 hiring option.

## Step 5 — Explain identity and permission separation

Before Microsoft connection, explain that:

- TeamMates sign-in establishes platform identity;
- Microsoft connection separately grants delegated source access;
- connected Microsoft tenant/object identifiers remain separate from TeamMates platform identity;
- a connected mailbox or calendar never grants TeamMates organisation membership;
- current access is `Mail.Read` and `Calendars.Read` only;
- TeamMates does not currently send email, change calendar events, access files or contact people.

Consent language must describe actual current capability, not target-state ambitions.

## Step 6 — Connect Microsoft Mail

The authorised owner starts the separate delegated Microsoft Mail connection.

The flow must:

- bind state and PKCE to the authenticated owner;
- use the approved multi-tenant Microsoft Mail application boundary;
- request delegated `Mail.Read` only;
- verify tenant and object identity;
- preserve the separation from platform organisation membership;
- fail closed on state, identity or permission mismatch;
- record safe connection and failure evidence without logging message content.

## Step 7 — Connect Microsoft Calendar

Where calendar workflows are included, the authorised owner connects the separate delegated calendar boundary.

The flow must:

- request delegated `Calendars.Read` only;
- verify the exact application and secret boundary;
- avoid `Calendars.ReadWrite` and application permissions;
- avoid invitation or attendee communication;
- expose connection health truthfully.

## Step 8 — Confirm first-use preferences and facts

Ask only for information necessary to produce safe first work, such as:

- which mailbox/account is connected;
- working-day or briefing preferences where already supported;
- explicit owner notes or request facts for a selected workflow;
- confirmed communication preferences for a controlled draft;
- acknowledgement of the review-only boundary.

Do not create broad permanent memory from observed edits without explicit confirmation.

## Step 9 — Readiness checks

Before Probation starts, validate:

- organisation membership;
- TeamMate configuration;
- lifecycle and entitlement;
- Microsoft connection health;
- required delegated permissions;
- feature flags and controlled-principal restrictions;
- database and queue dependencies;
- required reasoning-provider configuration for any enabled draft path;
- customer understanding of the control model.

A failed prerequisite keeps the TeamMate in Configuring and gives a safe, actionable explanation.

## Step 10 — Enter Probation

Probation begins only after required readiness checks pass.

Record:

- who initiated Probation;
- the exact role/version and configuration;
- connected source identities;
- current permission set;
- enabled workflows and feature gates;
- the readiness evidence;
- the start time.

## Step 11 — Deliver first useful work

The onboarding path should reach one safe, meaningful customer outcome as early as practical, such as:

- a grounded Morning Briefing;
- an Important Email recommendation or controlled review-only draft;
- a Meeting Preparation brief;
- a Meeting Follow-Up item from explicit notes;
- an Overdue Action recommendation;
- a Document Request internal draft.

The customer should see the item in Today or Work Queue, understand the source and complete the appropriate review or dismissal.

## Step 12 — Explain Activity and controls

The customer must be shown:

- where prepared work appears;
- how to identify its source and evidence;
- how Needs Your Input works;
- what finishing review or dismissal means;
- that no external send or mutation occurs;
- where truthful Activity history appears;
- how to pause or disconnect.

# 7. Probation operating rules

During Probation:

- workflows remain within the current release boundary;
- important outputs are reviewable;
- uncertainty and missing information are prominent;
- behaviour may be more explanatory than after trust is established;
- no additional permission or autonomy is granted automatically;
- a customer edit does not silently become a permanent preference;
- incidents, unsupported facts and unsafe commitments are treated as readiness evidence;
- support contact should be easy to find.

A default period of approximately seven calendar days may be used as a planning hypothesis, but elapsed time alone never completes Probation.

# 8. Probation evidence

Readiness evidence should include, where applicable:

## Identity and tenancy

- supported sign-in succeeded;
- exact organisation membership resolved;
- wrong-tenant and unknown-user paths fail closed.

## Integration

- delegated permissions match the current boundary;
- connection and refresh paths are healthy;
- revocation and disconnect behaviour are understood;
- no write scope or application permission is present.

## Workflow

- at least one eligible live-business item completes end to end;
- source and evidence remain visible;
- Work Queue and Activity agree;
- exact replay is idempotent;
- stale and Suspended cases fail safely.

## Customer understanding

The owner can explain:

- what Admin TeamMate can access;
- what it cannot access;
- what a review action does;
- that nothing is currently sent or changed externally;
- how to pause and get support.

## Quality and trust

- no unresolved P0 safety, tenant or data-integrity defect;
- no unresolved material permission ambiguity;
- outputs are useful enough to continue;
- known limitations and residual risks are recorded.

# 9. Probation review

The review should present:

- enabled workflows and their observed outcomes;
- connection and permission state;
- customer usage and review completion;
- quality defects and support issues;
- unresolved Needs Your Input patterns;
- customer understanding and confidence;
- recommendation: remain in Probation, move to Active, Suspend or Archive.

The decision and evidence must be auditable.

# 10. Exit to Active

Admin TeamMate may move to Active only when:

- required integrations remain healthy;
- current permissions are correct;
- the owner has completed the required first-use journey;
- core current workflows have acceptable evidence;
- no release-blocking issue remains for that environment/customer;
- the customer understands the human-control model;
- the customer confirms readiness where required;
- policy permits transition.

Moving to Active does not:

- add Microsoft permissions;
- enable email sending;
- enable calendar write;
- enable file access;
- remove required human review;
- activate a default-off feature;
- approve production release.

# 11. Remain in Probation

Keep the TeamMate in Probation when:

- first value has not been demonstrated;
- customer configuration or input is incomplete;
- a non-critical integration issue is being resolved;
- output quality needs further controlled observation;
- the customer does not yet understand the control model;
- the customer wants more time before Active status.

State the exact remaining criteria rather than extending Probation indefinitely without explanation.

# 12. Suspension and pause

The owner should be able to pause Admin TeamMate through clear customer language.

On pause:

- status becomes Suspended with `customer_paused` reason;
- no new work starts;
- scheduled work stops where appropriate;
- no external effect can execute;
- configuration and durable work remain preserved;
- the experience explains what is paused and what remains stored;
- Activity records the lifecycle change.

Reactivation must revalidate:

- entitlement;
- organisation membership;
- integration health;
- delegated permissions;
- policy;
- current role/version and configuration;
- unresolved security or incident blocks.

# 13. Disconnect

Disconnecting Microsoft access must:

- identify the exact connection affected;
- revoke or remove the applicable credential/consent path where technically supported;
- stop workflows that require the source;
- preserve only data required by policy and retention rules;
- avoid implying that platform membership is removed;
- provide a truthful Activity record;
- explain any retained evidence or pending deletion process.

# 14. Failure and recovery states

## Identity failure

Block access without disclosing tenant information. Direct the user to the appropriate organisation or support route.

## Permission denied or revoked

Explain which current workflow is unavailable and how to reconnect. Do not request broader permission as a shortcut.

## Integration unavailable

Preserve existing durable state, avoid duplicate work and show a safe retry/recovery state.

## Reasoning unavailable

Keep the source and work item safe, show that draft preparation could not complete and avoid a fabricated fallback.

## Stale source or item

Refuse the mutation, refresh safely and ask the customer to review the current version.

## TeamMate Suspended

Do not start or resume work until reactivation passes all checks.

# 15. Accessibility and support

Onboarding must:

- target WCAG 2.2 AA;
- work with keyboard and assistive technology;
- use clear labels and error summaries;
- avoid relying on colour alone;
- support mobile web for essential review and recovery actions;
- present a visible support or escalation route;
- avoid technical Azure, Graph, queue or model jargon in normal customer copy.

# 16. Onboarding measures

Track:

- start-to-sign-in completion;
- organisation-membership resolution;
- Microsoft Mail and Calendar connection completion;
- permission-denial and abandonment reasons;
- time to Probation;
- time to first useful work;
- time to first completed review;
- customer comprehension of the current boundary;
- probation duration and outcome;
- support effort and recurring blockers;
- pause, disconnect and reactivation success.

Do not treat account creation or consent alone as activation.

# 17. Current internal-alpha gate

For the pinned SME v1 release candidate, onboarding and probation evidence contributes to `teammatesiq/platform#109`.

The gate requires signed-in live acceptance for Morning Briefing and the controlled customer paths, including Important Email acceptance under #88, together with Today/Work Queue/Activity consistency and release evidence.

Production or external beta onboarding remains blocked until the separate Founder launch decision.

# 18. Change control

A material onboarding change requires review when it affects:

- identity or organisation membership;
- requested Microsoft permissions;
- lifecycle transition;
- data collection or retention;
- customer claims or consent language;
- external effects;
- activation, trial or billing status;
- accessibility of a critical journey.

Founder approval is required for scope, permission, material risk or production-launch changes.

# 19. Related documents

- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Role Handbook](admin-teammate-role-handbook.md)
- [Admin TeamMate Workflows](admin-teammate-workflows.md)
- [Admin TeamMate UX/UI Specification](../ux/admin-teammate-ux-ui-specification.md)
- [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)