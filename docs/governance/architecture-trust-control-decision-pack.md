---
Document title: TeamMates SME v1 Architecture and Trust-Control Decision Pack
Version: 1.0
Status: Approved
Owners: Head of Software / Solution Architect; Security & Governance Lead; Data & Integrations Lead
Orchestrator: Programme Director / Product-Technology Orchestrator
Last updated: 2026-08-09
---

# 1. Purpose

This pack records the approved architecture, security and integration decisions required to implement the approved SME v1 Product decisions without allowing runtime, AI, frontend or provider behaviour to redefine them.

The pack closes the design questions identified by `PBR-B03`, `PBR-B08`, `PBR-B10`, `PBR-B13`, `PBR-H01`, `PBR-H02` and `PBR-H10`. It does not approve a technology vendor, hosting platform, commercial package, legal basis or production release.

ATC-001 through ATC-008 were explicitly approved and became Active on 2026-08-09. Their required evidence remains a release gate and is not implied by decision approval.

# 2. Binding Product Context

- **P-001:** Admin TeamMate is the only commercial TeamMate in the UK SME v1 MVP.
- **D-001:** The deployed lifecycle is exactly Configuring → Probation → Active → Suspended → Archived. Customer-facing Paused maps to `suspended / customer_paused` and is not a separate state.
- **PD-001:** One authenticated Organisation Owner holds all v1 operating authority.
- **PD-002:** Probation is live and supervised. Active grants no additional permissions. Suspension fences execution and Archive is terminal.
- **PD-003:** Pause, Microsoft disconnect, source removal, TeamMate offboarding and Organisation closure are distinct operations.
- **PD-004:** Today is a projection. The Work Queue is the durable work record with four deterministic primary groups.
- **PD-005:** The only v1 external write is an email sent after the Owner approves the exact final payload. Outlook drafts are excluded.
- **PD-006:** Activation occurs on entry to Probation; exit and beta evidence are criteria-based.
- **PD-007:** The private beta is restricted to the approved UK, single-user, Microsoft 365 and data eligibility boundary.

# 3. Active Decisions

## ATC-001 — Deterministic Authority, Tenant Context and Runtime Boundary

TMOS, not the model or frontend, is authoritative for identity, tenant context, lifecycle, permissions, policy, approvals and external execution.

1. Every customer request is authenticated as the Organisation Owner and resolved server-side to exactly one `organisation_id`.
2. The client must not supply an authoritative tenant identifier. Any tenant identifier in a route or payload is treated only as a resource reference and must match the authenticated context.
3. Every tenant-scoped record carries `organisation_id`. PostgreSQL row-level security supplements application authorisation on all tenant business tables.
4. API requests, scheduled jobs and workers establish tenant context from a trusted, signed execution envelope. A worker must fail closed if the tenant, TeamMate, workflow or control version cannot be resolved.
5. AI output is a structured proposal only. The model cannot grant permission, alter policy, approve work, change lifecycle or call Microsoft Graph directly.
6. Provider adapters can be invoked only by an authorised TMOS application service after deterministic checks.
7. Elevated operational access is not an ordinary application path. Any future support-access path requires a separate, time-bound, reason-bound and fully audited control before live beta.

**Required evidence:** tenancy/RLS ADR; tenant-table matrix; worker-context contract; negative cross-tenant tests; proof that model and frontend paths cannot invoke connectors directly.

## ATC-002 — Lifecycle Capability Matrix and Transition Enforcement

Lifecycle is enforced by a single domain transition service using optimistic concurrency and an immutable audit event. Direct status updates are prohibited.

| Lifecycle state | Permitted customer work | Controlled external email | Platform-only activity |
|---|---|---|---|
| Configuring | Identity, connection, source, policy and configuration setup; safe validation only | Prohibited | Security, audit, connection validation and retention controls |
| Probation | Authorised read, retrieval, analysis and preparation workflows | Permitted only under ATC-003 and ATC-004 | Normal platform controls |
| Active | The same authorised work catalogue as Probation | Permitted only under ATC-003 and ATC-004 | Normal platform controls |
| Suspended | No new, queued, scheduled or resumed customer work | Prohibited | Security, audit, retention, reconciliation of already-submitted effects and reactivation validation only |
| Archived | No customer work | Prohibited | Statutory or contractual retention, rights handling and audit preservation only |

Required implementation rules:

1. Store `status`, `lifecycle_version`, `control_epoch`, transition timestamps and `suspended_from_status` for a suspension originating from Configuring, Probation or Active.
2. Store suspension causes as auditable records. `suspension_reason` is the current primary projection, not evidence that no other blocking cause exists.
3. Reactivation is allowed only when every blocking cause is cleared and identity, entitlement, Microsoft connection, permissions, policy, configuration and source authority revalidate.
4. Reactivation returns to `suspended_from_status`; it never assumes Active. Active cannot return to Probation in v1.
5. Archive first performs the suspension fence, then completes offboarding and atomically records the terminal transition. Archived cannot reactivate.
6. A transition conflict returns a deterministic concurrency error and never overwrites a newer lifecycle decision.

For the primary suspension projection, use this precedence: `security_suspension`, `admin_suspended`, `integration_disconnected`, `subscription_suspended`, `trial_expired`, `customer_paused`. The precedence affects presentation only; all causes must be cleared before reactivation.

**Required evidence:** lifecycle ADR; transition table; database constraints; concurrency tests; state-capability tests; Archive irreversibility test.

## ATC-003 — Suspension Fence and Stale-work Control

Suspension must fence work at every material execution boundary, not only at workflow creation.

1. On suspension, TMOS atomically increments `control_epoch`, records the cause, prevents new scheduling and marks non-started work as fenced or cancelled according to its workflow contract.
2. The Runtime rechecks lifecycle and `control_epoch` before queue publication, worker claim, material AI execution, approval creation, approval consumption and connector invocation.
3. Work claimed under an earlier epoch cannot produce a visible artefact or external effect. Safe intermediate computation may finish, but its result is discarded or quarantined and audited.
4. Every pending approval created under an earlier epoch becomes stale and cannot be consumed after reactivation.
5. An external request submitted before the suspension cannot be recalled by TMOS. It is reconciled under ATC-004 and clearly shown as an already-submitted outcome.
6. Platform maintenance during suspension cannot act on behalf of the TeamMate or create a controlled external action.

**Required evidence:** suspension-fencing ADR; queue lease/claim contract; stale-epoch tests at every boundary; race tests for approve-versus-pause and send-versus-pause.

## ATC-004 — Payload-bound Approval Integrity

Email approval is immutable, single-use, Owner-only and bound to one exact payload and control context.

The approval digest must cover a canonical representation of:

- Organisation, TeamMate, workflow and action identifiers;
- sender mailbox;
- `to`, `cc` and `bcc` recipients in canonical order;
- subject and body, preserving the approved content type;
- attachment identifiers, names, media types, sizes and cryptographic content digests;
- reply/thread reference where applicable;
- applicable policy, permission, Blueprint, DNA and workflow versions; and
- lifecycle `control_epoch`.

Approval rules:

1. Only the authenticated Organisation Owner may approve.
2. Approval expires 15 minutes after approval or earlier if any bound value, authority, lifecycle, connection, permission, policy or source state changes.
3. Any material edit creates a new payload version and invalidates the prior approval. The model cannot decide that an edit is immaterial.
4. Approval and rejection are concurrency-safe terminal decisions for that approval version.
5. Approval does not itself send. A separate execution service consumes the approval once after rechecking identity, lifecycle, epoch, entitlement, connection, permission, policy, payload digest and expiry.
6. Consumption is recorded before provider invocation under a unique action-attempt key. The same approval cannot authorise a second attempt.
7. Display text must show the exact sender, recipients, subject, body, attachments and consequences presented for approval.

**Required evidence:** controlled-action/approval ADR; canonicalisation specification; immutable approval schema; approve/edit/race/expiry/bypass tests; cryptographic digest test vectors.

## ATC-005 — External Email Attempt, Reconciliation and Customer Semantics

TMOS is the system of record for the prepared email payload. Outlook drafts remain excluded.

The execution adapter uses Microsoft Graph `sendMail` with `saveToSentItems = true`. The state machine is:

`prepared → awaiting_approval → approved → submitted → sent | indeterminate`

Terminal rejection, cancellation and failure outcomes remain explicit and are not presented as Completed success.

1. `approved` means the exact payload passed ATC-004. It is not an external outcome.
2. `submitted` means TMOS invoked Graph and received `202 Accepted`. It does not mean processing completed or delivery occurred.
3. `sent` means TMOS found a sufficiently exact matching item in the Owner mailbox Sent Items during a bounded reconciliation window. It means evidence of dispatch from the mailbox, not recipient delivery.
4. `indeterminate` means TMOS cannot safely establish whether the provider accepted or processed the attempt, including a timeout after request transmission or no unambiguous Sent Items match.
5. TMOS never displays `delivered` in v1 and never maps provider acceptance alone to Work Queue Completed.
6. A submitted or indeterminate attempt is never automatically retried. The Owner may inspect the evidence and initiate a new prepared payload; that creates a new approval and action attempt.
7. A failure known to have occurred before Graph could accept the request may be retried only by a deterministic worker under the same single attempt key and only while the approval remains valid. The adapter must distinguish this class from an uncertain transmission.
8. Reconciliation matching uses the immutable sender, recipient set, subject, canonical content digest, attachment metadata and a bounded submission time window. Ambiguous matches remain indeterminate.
9. Each attempt records request correlation, timestamps, provider response class, reconciliation evidence and final interpretation without logging access tokens or unnecessary message content.

Microsoft documents that `sendMail` returns `202 Accepted` without a response body and that this does not mean processing completed. This provider contract is the reason `submitted`, `sent` and `indeterminate` remain distinct.

**Required evidence:** Microsoft Integration Contract; send/reconciliation ADR; provider contract tests; lost-response, timeout, duplicate-prevention, ambiguous-match and suspension-race tests.

## ATC-006 — Microsoft Identity, Consent and Minimum Access

SME v1 uses delegated Microsoft access for the authenticated Owner. Application-only mailbox or tenant access is prohibited.

1. Use Microsoft Entra ID authorisation-code flow with PKCE, server-side token handling and refresh-token support where permitted.
2. Bind the TMOS Owner, Microsoft tenant, Entra subject, mailbox and connection as one immutable connection identity. A connection cannot be moved between Organisations.
3. Mail and calendar calls use the Owner context (`/me`) and the minimum delegated capability set required by the approved catalogue: identity, mail read, mail send and calendar read. Calendar write scopes are prohibited.
4. Consumer Microsoft accounts, shared/delegated/group mailboxes, cross-tenant identities and application permissions are rejected by eligibility and runtime checks.
5. Tokens are encrypted at rest, never exposed to the client after exchange, rotated/revoked where supported and deleted or cryptographically rendered unusable on disconnect.
6. Disconnect immediately fences dependent workflows and adds `integration_disconnected` as a suspension cause. Webhooks, subscriptions, cached authority and refresh capability are revoked or expired.
7. Consent state, effective scopes, token health and mailbox identity are revalidated before controlled execution.
8. Consent is not permission to ingest every accessible resource. Product-selected source boundaries and ATC-007 still apply.

The exact Entra application registration, redirect URIs and scope strings must be recorded in the Microsoft Integration Contract and verified in a non-production tenant before implementation approval.

**Required evidence:** Microsoft access ADR; consent/scope matrix; token lifecycle and disconnect state machine; test-tenant evidence; revoked-consent and wrong-tenant tests.

## ATC-007 — Selected Knowledge Sources, ACL and Revocation

Knowledge access is read-only and deny-by-default.

1. Do not request `Files.Read.All`, `Files.ReadWrite.All`, `Sites.Read.All` or `Sites.ReadWrite.All` for SME v1.
2. Use Microsoft Selected permissions in delegated mode with an explicit read assignment to each approved site, list, folder or file, choosing the narrowest operationally supported resource level.
3. Both the Owner's Microsoft authority and the application assignment must permit access. TMOS never broadens the Owner's native authority.
4. Source selection records the provider tenant, site/drive/item identifiers, assignment evidence, Owner authority, sensitivity classification, version/change token and ingestion status.
5. Retrieved chunks retain source and ACL lineage. Retrieval checks current source authority and freshness; vector similarity alone never grants access.
6. Source removal immediately blocks retrieval, revokes the application assignment where supported, invalidates derived retrievable content and records lineage-preserving tombstones required for audit.
7. If Selected permissions cannot be provisioned and validated for a beta customer, that source is unavailable. The implementation must not silently widen OAuth scope; any broader-access proposal returns to Product, Security, Legal and Programme decision control.

Microsoft's Selected permissions model requires both consent and explicit resource assignment; consent alone grants no resource access.

**Required evidence:** source-access/ACL ADR; Selected-permission provisioning proof; ACL/lineage schema; source removal and stale-authority tests; negative access tests.

## ATC-008 — Transaction, Event and Audit Reconstruction Boundary

Business state, reliable events and audit evidence must support reconstruction without treating logs as the source of truth.

1. PostgreSQL is the transactional source of truth for TeamMate lifecycle, workflow/task state, approvals, controlled-action attempts, source authority and audit metadata.
2. A transactional outbox record is committed in the same transaction as every state change that requires asynchronous continuation.
3. Consumers are at-least-once and idempotent. A unique business key prevents duplicate workflow, approval and external-action effects.
4. Audit events are append-only and include Organisation, actor/source, TeamMate, workflow/task/action, event type, prior/new state where applicable, policy/permission/control versions, correlation and causation IDs, time and evidence references.
5. Sensitive payloads are minimised and stored separately under their applicable encryption, access and retention controls; the audit event retains a digest/reference sufficient for reconstruction.
6. The model cannot write audit events directly. TMOS records the model request/result metadata and the deterministic decision made from it.
7. Retention periods remain a Legal decision. Architecture must support policy-based retention, legal hold where required and verifiable deletion without deleting records that must lawfully persist.

**Required evidence:** persistence/outbox ADR; normative event and audit schemas; append-only enforcement; replay/idempotency tests; one end-to-end reconstruction test for an approved email attempt.

# 4. Required ADR Set

Approval of this pack authorises the Head of Software to create, but does not itself accept, the following focused ADRs:

| ADR subject | Decisions implemented |
|---|---|
| Tenant Context, RLS and Trusted Worker Envelope | ATC-001 |
| Lifecycle Transition Service and Suspension Fence | ATC-002, ATC-003 |
| Controlled-action Approval Integrity | ATC-004 |
| Microsoft Email Send and Reconciliation | ATC-005 |
| Delegated Microsoft Access and Consent | ATC-006 |
| Selected Knowledge Access and ACL Lineage | ATC-007 |
| Transactional Outbox, Idempotency and Audit Reconstruction | ATC-008 |

Technology/vendor ADRs for hosting, queues, object storage, AI provider, secrets, observability, billing and disaster recovery remain separate decisions and are not authorised by this pack.

# 5. Conflicts Closed by Approval

| Finding | Closure effect |
|---|---|
| PBR-C01 / PBR-B03 | Replaces the incorrect `active`-only execution guard with the approved state-capability matrix and deterministic transition/fencing contract. |
| PBR-B02 / PBR-H01 | Makes the single Owner authority and tenant enforcement executable. |
| PBR-H02 | Defines payload binding, approver eligibility, expiry, concurrency and single-use consumption. |
| PBR-C07 / PBR-B13 | Makes Graph acceptance `submitted`, requires provider-side evidence for `sent`, prohibits `delivered` and prevents blind retry. |
| PBR-B10 / PBR-H03 | Defines delegated Microsoft access, consent, disconnect, selected-source access, ACL and revocation boundaries. |
| PBR-H10 | Defines the minimum event/audit reconstruction contract while retaining Legal authority over retention. |

The findings are not formally closed until the approved pack is propagated into the canonical Architecture, Security, Data/API, UX and Test specifications and the required evidence passes.

# 6. Impacts

## Product

No Product scope is expanded. Probation and Active have the same permission catalogue; Outlook drafts and delivery claims remain excluded. Indeterminate email outcomes require clear Owner handling.

## Architecture

Requires a single lifecycle service, control epochs, transactional outbox, tenant-context enforcement, immutable approval payload versions and provider reconciliation.

## UX

Must show exact approval payloads, approval expiry/staleness, lifecycle causes, sent-versus-delivered semantics, indeterminate email outcomes and reactivation validation without exposing internal security details.

## Security

Approval, tenant isolation, suspension and connector boundaries become deterministic controls with fail-closed behaviour and explicit negative tests.

## Data/API

Requires closed schemas and endpoints for lifecycle transitions, suspension causes, approvals, action attempts, Microsoft connections, source assignments, event outbox and audit evidence.

## Testing

Requires concurrency, tenant-isolation, approval-mutation, stale-work, duplicate-send, lost-response, consent-revocation, ACL and audit-reconstruction suites.

## Commercial

No customer-facing SLA or delivery guarantee is created. Some customers may need Microsoft resource-owner or administrator participation to grant Selected permissions; this must be reflected in beta qualification and onboarding.

# 7. Dependencies and Questions

1. Security must accept the 15-minute approval expiry and all fail-closed controls.
2. Data & Integrations must prove the delegated scope and Selected-permission model in a test Microsoft tenant before the Microsoft Integration Contract is accepted.
3. Legal must approve token, email-evidence, source-lineage, audit and retention treatment before live personal data.
4. UX must define customer language for `submitted`, `sent`, `indeterminate`, stale approvals and multiple suspension causes.
5. QA must convert every Required evidence item into traceable acceptance and adversarial tests.
6. Product approval is required for any proposal to create Outlook drafts, widen Microsoft access, add a controlled action or claim delivery.

# 8. Repository Changes Required After Approval

- Record ATC-001 through ATC-008 as Active in `docs/governance/decision-register.md`.
- Create the seven ADRs listed in section 4 under `engineering/adr/`.
- Create the Microsoft Integration Contract.
- Align `docs/architecture/tmos-system-architecture.md` and `docs/architecture/tmos-domain-model.md`.
- Align `docs/security/security-privacy-governance.md`.
- Close the relevant contracts in `docs/engineering/api-contract-service-interfaces.md` and `docs/engineering/data-model-database-schema.md`.
- Update the Workflow, Onboarding/Probation and UX specifications.
- Add requirements-to-test traceability and the required evidence suites.
- Update the Programme Baseline Audit Report only when closure evidence exists.

# 9. Approval Record

| Approval | Status |
|---|---|
| Head of Software / Solution Architect | Recommendation accepted through explicit programme approval on 2026-08-09 |
| Security & Governance Lead | Recommendation accepted through explicit programme approval on 2026-08-09 |
| Data & Integrations Lead | Recommendation accepted through explicit programme approval on 2026-08-09 |
| Programme reconciliation | Approved and recorded on 2026-08-09; ATC-001 through ATC-008 are Active |

# 10. Execution Readiness

- Ready for Lovable: No
- Ready for Codex: Yes, for the seven ADRs and Microsoft Integration Contract only
- Decision required first: No for the authorised contract-authoring scope; Yes before feature implementation if the accepted contracts expose a material unresolved choice
- Authorised execution scope: The seven ADRs in section 4 and the Microsoft Integration Contract only
- Feature implementation remains blocked pending accepted contracts, aligned specifications and traceable test evidence.

# 11. Related Documents

- [Approved Product Decision Pack](product-decision-pack.md)
- [Decision Register](decision-register.md)
- [Programme Baseline Audit Report](programme-baseline-audit-report.md)
- [TMOS System Architecture](../architecture/tmos-system-architecture.md)
- [TMOS Domain Model](../architecture/tmos-domain-model.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)

## Provider References

- [Microsoft Graph `sendMail`](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0)
- [Microsoft Selected permissions for OneDrive and SharePoint](https://learn.microsoft.com/en-us/graph/permissions-selected-overview)
