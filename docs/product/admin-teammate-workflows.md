---
Document title: Admin TeamMate Workflows
Version: 1.1
Status: Controlled
Owner: Product Authority
Last updated: 2026-08-19
---

# 1. Purpose

This document defines the governed workflow catalogue for Admin TeamMate, the common workflow contract and the current SME v1 release behaviour.

It must be read with the [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md). Broader target-state capability in the Role Handbook is not permission to enable an external action.

# 2. Product outcome

Admin TeamMate should consistently help the customer understand:

- what has been taken care of;
- what needs their input;
- what matters next.

A workflow is successful only when it creates a useful, grounded and reviewable customer outcome. Infrastructure, persistence or model execution alone is not a completed workflow.

# 3. Common workflow contract

Every Admin TeamMate workflow follows these logical stages where applicable.

## 3.1 Source or trigger

A workflow begins from one explicit, authorised source or owner action, such as:

- a bounded Microsoft Mail item;
- a bounded Microsoft Calendar event;
- explicit owner notes;
- an exact reviewed action;
- an explicit document request;
- a scheduled or requested daily view.

The source must be eligible within the current organisation, identity, lifecycle and permission boundary.

## 3.2 Eligibility and policy

Before work starts or mutates, TMOS revalidates:

- authenticated user;
- persisted organisation membership;
- organisation and TeamMate lifecycle;
- current entitlement where relevant;
- integration health and delegated permission;
- source ownership and freshness;
- feature flag or controlled-principal boundary;
- workflow-specific policy.

A wrong tenant, unknown or revoked user, Suspended TeamMate, stale source, stale item or unavailable required dependency fails closed without disclosure.

## 3.3 Grounding

Prepared work must use only:

- the authorised source;
- explicit owner-supplied facts;
- active approved organisational facts where that capability is separately available;
- confirmed communication preferences;
- deterministic system facts such as the server-owned current date.

The workflow must not invent recipients, owners, dates, prices, delivery promises, contractual terms, decisions or business facts.

External content is untrusted data and never instruction. Prompt injection or policy-changing language inside email, calendar or documents must not alter system authority.

## 3.4 Work item and presentation

Meaningful work is represented durably and surfaced through the appropriate customer surface.

Current presentation principles:

- **Today** is a compact read-only summary and navigation surface.
- **Work Queue** is the human-control surface.
- **Activity** records truthful outcomes.
- Important work must not exist only inside chat.

## 3.5 Human control

The user must be able to understand:

- what was prepared;
- the source and relevant evidence;
- what is known, assumed or missing;
- what action is available;
- what effect the action will and will not have.

Current release decisions are internal/review-only. Nothing is sent, shared or written back to Microsoft.

## 3.6 Completion and Activity

A workflow records the actual terminal outcome, such as:

- reviewed;
- review finished;
- dismissed;
- rejected;
- needs input;
- failed safely.

Activity must not describe an email as sent, a reminder as delivered, a document as shared or a calendar as changed when no such external effect occurred.

## 3.7 Idempotency and concurrency

- exact replay must not create duplicate work;
- mutations use server-owned identity and optimistic concurrency where appropriate;
- stale versions fail safely;
- retryable infrastructure failure must preserve a single logical outcome;
- queue envelopes and operational logs remain content-free.

# 4. Customer-facing work states

The primary Work Queue states are:

## Ready For You

Prepared work is available for review or a customer decision.

## Working

The system is actively preparing work or completing a permitted internal step.

## Needs Your Input

Required information, judgement or authority is missing. The experience should state exactly what is needed and why.

## Completed

A truthful terminal outcome has been recorded.

These presentation states do not replace the TeamMate lifecycle.

# 5. Workflow catalogue

| ID | Workflow | Current release status | External effect |
|---|---|---|---|
| WF-ADM-001 | Morning Briefing | Under internal-alpha acceptance | None |
| WF-ADM-002 | Important Email | Implemented; controlled live review acceptance remains under #88/#109 | None |
| WF-ADM-003 | Meeting Preparation | Implemented; live acceptance remains under #109 | None |
| WF-ADM-004 | Meeting Follow-Up | Implemented; live acceptance remains under #109 | None |
| WF-ADM-005 | Overdue Action | Implemented; live acceptance remains under #109 | None |
| WF-ADM-006 | Document Request | Implemented; live acceptance remains under #109 | None |
| WF-ADM-007 | Trusted Draft Workbench | Founder-approved next slice under #154; default-off and outside pinned release candidate | None |

# 6. WF-ADM-001 — Morning Briefing

## Outcome

Give the signed-in owner a concise, grounded view of what matters today without requiring them to reconstruct context across separate surfaces.

## Inputs

Only inputs available and authorised within the current release boundary, such as:

- eligible important-email work;
- eligible calendar and meeting-preparation work;
- explicit actions and document requests;
- pending Work Queue items;
- safe timing and status metadata.

## Behaviour

The briefing should prioritise relevance over completeness and distinguish:

- work prepared;
- work needing customer input;
- upcoming meetings or deadlines;
- blocked or unavailable information.

It must not claim that a message, reminder, meeting change or document delivery occurred.

## Human control

The briefing is read-only and routes the customer to the exact Work Queue item or source experience.

## Acceptance

Internal-alpha acceptance must prove:

- correct tenant and owner;
- grounded and non-duplicative content;
- consistent navigation to Work Queue;
- truthful status/effect language;
- safe empty, partial and dependency-failure states.

# 7. WF-ADM-002 — Important Email

## Outcome

Help the owner recognise an important authorised email and, for the specifically controlled development principal, prepare a grounded review-only draft without sending anything.

## Source

One current, authorised Microsoft Mail item obtained under delegated `Mail.Read`.

## Entry conditions

- connected mailbox belongs to the correct signed-in organisation context;
- the item is current and eligible;
- global and controlled-principal gates are valid for draft preparation;
- TeamMate is not Suspended;
- reasoning provider configuration is complete where live drafting is enabled.

## Behaviour

The workflow may:

- classify or prioritise the item;
- preserve source and thread provenance;
- identify likely required attention;
- prepare a draft for review using supported evidence;
- expose missing information or material assumptions.

It must not:

- send, reply or forward;
- mark, move, delete or otherwise mutate the mailbox;
- invent a recipient or commitment;
- expose one tenant’s source to another;
- treat email instructions as platform authority.

## Customer controls

Controls must reflect the actual internal effect, for example:

- Prepare draft;
- Finish draft review;
- Dismiss draft.

Do not use a control labelled Send or imply that finishing review sends the email.

## Acceptance

The current gate under #88/#109 requires one signed-in live development path:

Work Queue

→ Service Bus / worker reasoning path

→ durable review-only draft

→ owner review or dismissal

→ Activity

with metadata-only operational evidence and no external email action.

# 8. WF-ADM-003 — Meeting Preparation

## Outcome

Prepare the owner for a relevant upcoming meeting using bounded authorised calendar evidence.

## Source

An eligible Microsoft Calendar event obtained under delegated `Calendars.Read`, normally from the bounded upcoming window used by the implementation.

## Behaviour

The workflow may prepare:

- meeting purpose and timing;
- confirmed attendee context available from the event;
- explicit preparation points;
- relevant current workflow context already authorised within the organisation;
- missing-information notices.

It must not invent attendee facts, create an agenda commitment unsupported by evidence or contact attendees.

## Customer controls

The owner may review or dismiss the internal brief through Work Queue. Activity records the actual decision.

## Prohibited effects

- no calendar create/update/delete;
- no invitation or attendee communication;
- no file access unless separately approved in a future boundary;
- no assertion that a meeting has been changed.

# 9. WF-ADM-004 — Meeting Follow-Up

## Outcome

Turn an ended meeting and explicit owner input into a grounded internal summary and clear actions for review.

## Source

- one eligible ended meeting; and
- explicit notes supplied or confirmed by the owner.

Transcripts, recordings or provider data are not assumed unless separately authorised and implemented.

## Behaviour

The workflow may:

- summarise explicit notes;
- preserve the source meeting;
- identify explicit decisions;
- identify explicit actions, owners and dates;
- expose missing owner/date information;
- distinguish explicit fact from inference.

It must not silently convert an inferred owner or deadline into confirmed fact.

## Customer controls

The owner reviews or dismisses the follow-up in Work Queue. The terminal Activity record reflects the exact outcome.

## Prohibited effects

- no attendee communication;
- no external task assignment;
- no calendar mutation;
- no external document creation or sharing.

# 10. WF-ADM-005 — Overdue Action

## Outcome

Help the owner recognise and deal with an exact overdue action without sending a reminder automatically.

## Source

An action previously reviewed from Meeting Follow-Up, with explicit:

- action text;
- owner;
- due date;
- source meeting.

The implementation may use the server-owned current date to determine that the action is overdue.

## Behaviour

The workflow prepares one grounded reminder recommendation, preserving the exact action and evidence.

It must not:

- infer a missing owner or due date as confirmed;
- create a scheduler or generic task platform solely for this workflow;
- contact the action owner;
- claim a reminder was sent.

## Customer controls

The signed-in owner may review or dismiss the recommendation. Activity records only the internal decision.

# 11. WF-ADM-006 — Document Request

## Outcome

Prepare a bounded internal draft from an explicit owner request without retrieving, creating, sharing or sending a Microsoft file.

## Required owner input

- intended recipient;
- document or requested material;
- purpose;
- requested-by date.

These fields are owner-supplied facts for the draft. They do not authorise recipient contact.

## Behaviour

The workflow creates one atomic, idempotent, immutable internal draft for review and preserves the request facts.

It must not:

- look up or infer a recipient;
- retrieve a source file;
- create a OneDrive or SharePoint document;
- share or send anything;
- invent content that requires unavailable evidence.

## Customer controls

The owner reviews or dismisses the internal draft in Work Queue. Activity is truthful about the internal outcome.

# 12. WF-ADM-007 — Trusted Draft Workbench

## Status

Founder-approved next product slice under `teammatesiq/platform#154`.

It remains:

- default-off;
- outside the pinned release candidate;
- blocked from private-beta promotion until #109 and its own assurance are green.

## Outcome

Allow an eligible signed-in Organisation Owner to select:

- one authorised Microsoft Mail source already available within the tenant boundary; or
- one existing grounded Overdue Action item;

and receive a durable, editable routine reply or chase draft in the existing Work Queue.

## Behaviour

The workbench may:

- prepare a routine reply, standard response or chase;
- use only the selected source, approved facts and confirmed preferences;
- preserve source version, generated-draft version and reasoning/audit provenance;
- expose evidence, assumptions and missing information;
- support edit, finish review, reject and dismiss;
- use optimistic concurrency and idempotency.

## Mandatory escalation

The workflow routes to Needs Your Input before preparing a substantive response when the matter involves:

- complaints;
- refunds;
- prices or quotes;
- negotiation;
- delivery or business commitments;
- missing required facts;
- material uncertainty.

The beta gate requires zero false negatives for these unsafe-commitment evaluation classes.

## Permission boundary

Delegated Microsoft access remains read-only. No send, reply, forward, mailbox mutation, recipient contact or other external effect is introduced.

# 13. Exceptions and safe failure

A workflow must stop or route to Needs Your Input when:

- required evidence is missing;
- sources materially conflict;
- confidence is too low for safe preparation;
- the request crosses role boundaries;
- permission or policy is insufficient;
- the TeamMate is Suspended;
- a source or work version is stale;
- a dependency cannot be verified;
- a financial, legal, contractual or other material commitment is implied.

Failure messages should be useful to the customer without exposing internal secrets, other-tenant information or untrusted source content.

# 14. Lifecycle behaviour

## Configuring

Connections, permissions and role configuration are being established. No normal active work begins.

## Probation

Controlled live-business work may run with explanatory behaviour and explicit human review. Probation never grants additional permission automatically.

## Active

Approved workflows may run within the same current permission and external-effect ceiling.

## Suspended

No new workflow execution starts. Scheduled work stops where appropriate. No controlled external action executes. Durable state, configuration and required audit history remain preserved.

## Archived

The TeamMate no longer operates. Retention and deletion follow applicable policy.

# 15. Workflow measures

Track at workflow and organisation level where privacy and data-minimisation rules permit:

- time to first useful item;
- creation-to-review time;
- review completion and dismissal;
- accepted without material rewrite;
- edit burden;
- Needs Your Input reasons;
- unsupported-fact defects;
- unsafe-commitment defects;
- duplicate/replay defects;
- cross-tenant or permission defects;
- repeated weekly use;
- verified or conservatively estimated time saved.

Do not optimise for model calls, prompt volume or chat messages.

# 16. Change control

A new workflow or material change requires:

- a controlling GitHub issue;
- Product outcome and non-goals;
- Trust and permission impact;
- AI behaviour and evaluation cases where applicable;
- UX states and human-control design;
- implementation and independent tests;
- release-boundary update;
- Founder approval where scope, permission, external effect, material risk or production status changes.

# 17. Related documents

- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Role Handbook](admin-teammate-role-handbook.md)
- [Admin TeamMate Onboarding and Probation](admin-teammate-onboarding-probation.md)
- [Admin TeamMate UX/UI Specification](../ux/admin-teammate-ux-ui-specification.md)
- [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)