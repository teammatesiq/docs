---
Document title: Microsoft 365 Integration Contract — SME v1
Version: 1.0
Status: Proposed
Owners: Data & Integrations Lead; Head of Software / Solution Architect; Security & Governance Lead
Last updated: 2026-08-09
Implements: PD-003, PD-005, PD-007, ATC-003 to ATC-007
---

# 1. Purpose and authority

This contract defines the normative Microsoft identity, Graph access, controlled email-send, reconciliation, selected-source and disconnect behaviour for the TeamMates SME v1 private beta.

It does not widen Product scope. Admin TeamMate is the only v1 TeamMate; Outlook drafts, calendar writes, shared mailboxes, application permissions and recipient-delivery claims remain excluded.

# 2. Eligibility boundary

One TMOS Organisation Owner connects one Microsoft 365 work or school account in one Entra tenant and one primary user mailbox.

Reject:

- consumer Microsoft accounts;
- guest/cross-tenant identities where the token tenant is not the approved resource tenant;
- shared, delegated or group mailboxes;
- application-only access;
- connections whose Entra tenant, subject or mailbox cannot be bound unambiguously; and
- customers outside the approved PD-007 beta eligibility boundary.

# 3. Entra application registration

| Control | Normative requirement |
|---|---|
| Account type | Organisational-directory accounts only |
| OAuth flow | Authorisation code with PKCE |
| Token exchange | Server-side only |
| Implicit/hybrid grants | Disabled |
| Application permissions | None |
| Redirect URIs | Exact HTTPS allowlist per environment; no wildcard |
| Production localhost URI | Prohibited |
| Client secret in browser | Prohibited |

The precise client IDs, publisher verification, tenant authority and redirect URIs must be added to the environment register below after the hosting ADR is accepted. They are release-blocking configuration, not values to infer in code.

| Environment | Entra client ID | Tenant authority | Redirect URI | Status |
|---|---|---|---|---|
| Development | TBD | `organizations` or approved test tenant | TBD | Blocked by environment decision |
| Staging/test tenant | TBD | Exact test tenant ID | TBD | Blocked by environment decision |
| Production | TBD | `organizations`, then bound tenant validation | TBD | Blocked by hosting decision |

# 4. Delegated scope matrix

| Scope | Purpose | Condition |
|---|---|---|
| `openid` | Sign-in identity | Always |
| `profile` | Basic identity claims | Always |
| `offline_access` | Refresh token for authorised background work | Always |
| `User.Read` | Resolve `/me` and immutable identity binding | Always |
| `Mail.Read` | Approved inbox workflows and Sent Items reconciliation | Email capability enabled |
| `Mail.Send` | Approved exact-payload email send | Controlled email enabled |
| `Calendars.Read` | Read Owner calendar for approved admin workflows | Calendar-read capability enabled |
| `Files.SelectedOperations.Selected` | Read explicitly assigned files | Only for file sources; admin consent/assignment proven |
| `ListItems.SelectedOperations.Selected` | Read explicitly assigned items/folders | Only for item/folder sources; admin consent/assignment proven |
| `Lists.SelectedOperations.Selected` | Read an explicitly assigned list/library | Only for list/library sources; admin consent/assignment proven |
| `Sites.Selected` | Read an explicitly assigned site | Exception where narrower scope is unsupported and reason recorded |

Prohibited scopes include all application permissions, `Mail.ReadWrite`, `Mail.Send.Shared`, `Calendars.ReadWrite`, `Calendars.Read.Shared`, `Files.Read.All`, `Files.ReadWrite.All`, `Sites.Read.All` and `Sites.ReadWrite.All`.

Tenant administrators may impose consent requirements beyond Microsoft's default. TMOS reports this as administrator action required and never bypasses it.

# 5. Connection identity and token lifecycle

The connection record binds:

- `organisation_id` and TMOS Owner ID;
- Entra tenant ID and subject/object identity;
- Graph user ID, primary mailbox address and connection version;
- granted scopes and consent time;
- encrypted refresh-token reference and token health; and
- connection status, validation time and disconnect evidence.

Tokens remain server-side, encrypted at rest and excluded from logs, audit payloads and client responses. Refresh uses rotation when a replacement refresh token is issued. A tenant, subject or mailbox mismatch fails closed and adds the integration-disconnected suspension cause.

Before email submission, TMOS must validate the current connection version, tenant, Owner/mailbox identity, `Mail.Send`, `Mail.Read`, token health and TeamMate control epoch.

# 6. Controlled email request

Endpoint: `POST https://graph.microsoft.com/v1.0/me/sendMail`.

The adapter submits only the immutable payload consumed under ADR-013. `saveToSentItems` is omitted so Microsoft's documented default remains `true`; it is never set to `false`. The request may include a non-secret attempt correlation marker only where non-production proof confirms Microsoft retains it for reconciliation.

The provider adapter has no generic automatic retry wrapper.

| Provider outcome | TMOS interpretation | Retry rule |
|---|---|---|
| `202 Accepted` | `submitted` | Never resubmit this attempt |
| Deterministic 4xx before acceptance | Known failure | No automatic retry; correct and reapprove if payload/control changes |
| `401`/`403` | Connection/permission failure and execution fence | No send retry until reconnected/revalidated; old approval becomes stale |
| `429` before transmission is proven | Known pre-transmission failure | Bounded retry under same attempt key and valid approval, respecting `Retry-After` |
| 5xx before transmission is proven | Known pre-transmission failure | Bounded retry under same attempt key and valid approval |
| Timeout, connection loss or uncertain transmission | `indeterminate` | Never retry automatically |

An implementation that cannot prove the request was not transmitted must classify the result as indeterminate.

# 7. Email attempt state contract

Allowed success path:

`prepared -> awaiting_approval -> approved -> submitted -> sent`

`submitted -> indeterminate` is allowed after bounded reconciliation. `approved -> indeterminate` is allowed when transmission was attempted but no response established acceptance. Rejected, cancelled, expired and known-failure outcomes are explicit non-success states.

`submitted` and `sent` are not “delivered”. Work Queue success wording must follow PD-004 and UX approval; provider acceptance alone cannot produce Completed.

# 8. Sent Items reconciliation

Reconciliation begins after submission using the same bound Owner mailbox. It uses a bounded schedule and stops no later than 15 minutes after submission unless test-tenant evidence supports a shorter accepted window.

Candidate matching uses:

- sender mailbox and submission time window;
- canonical `to`, `cc` and `bcc` sets where visible;
- exact subject;
- approved content digest or a provider-normalisation-safe digest proven in test;
- attachment names, sizes and content digests where Graph exposes sufficient evidence; and
- the attempt correlation marker where its retention is proven.

Exactly one sufficiently exact candidate yields `sent`. Zero candidates at window end or multiple credible candidates yield `indeterminate`. Reconciliation evidence records Graph message ID, Internet message ID where available, Sent Items time and evidence digests/references; it does not duplicate full content into audit logs.

# 9. Selected knowledge sources

Consent and resource assignment are separate. A selected scope without an assignment grants no source access; an assignment cannot exceed the signed-in Owner's native authority.

Provisioning follows:

1. Owner selects the requested source in TMOS.
2. TMOS records the provider identifiers but marks the source unavailable.
3. An authorised customer administrator grants the runtime application `read` to the exact resource using an approved external admin process.
4. TMOS verifies the assignment and Owner authority in the test request.
5. Only then may ingestion begin.

The runtime app cannot grant itself resource access. If the customer cannot provision Selected permissions, the source remains unavailable.

# 10. Synchronisation and lineage

Only approved sources are synchronised. Initial ingestion and subsequent delta/change-token processing must preserve source version, provider identifiers, ACL/assignment evidence, content digest, retrieved time and connection version.

Webhook/subscription use is optional until separately designed; polling or delta sync must remain bounded and honour Graph throttling. No implementation may silently introduce application permissions to support background sync.

Before retrieval, TMOS checks source status, current connection version, current assignment, Owner authority and freshness. Stale or unverifiable content is denied, not merely labelled.

# 11. Disconnect, revocation and source removal

Microsoft disconnect:

1. atomically marks the connection disconnecting/disconnected;
2. adds `integration_disconnected` and increments the lifecycle epoch;
3. stops new sync and execution, stales approvals and fences queued work;
4. revokes tokens where supported and cryptographically destroys local refresh capability;
5. stops subscriptions/webhooks and invalidates cached authority; and
6. audits completion and any provider-side revocation uncertainty.

Source removal immediately denies retrieval, cancels its sync and attempts explicit assignment revocation. Derived chunks become non-retrievable immediately; physical deletion follows the approved Legal retention policy.

Reconnection is a new connection version. It cannot revive approvals, work or sources from the previous version without explicit revalidation.

# 12. Error and throttling semantics

Graph `429` and service-limit responses honour `Retry-After` for read/sync operations. Read operations use bounded exponential backoff with jitter and idempotent continuation tokens. Controlled sends follow section 6 and never retry when transmission is uncertain.

Customer-visible errors distinguish: administrator consent required, permission missing, connection expired, source assignment missing, provider temporarily unavailable, send outcome indeterminate and reconnection required.

# 13. Audit and data minimisation

Record correlation/causation IDs, connection/source/attempt versions, scope/assignment evidence, Graph request class, status code, provider correlation headers where available, timing and deterministic interpretation.

Never log access or refresh tokens, authorisation codes, PKCE verifiers or unnecessary message/source content. Content evidence is stored separately under encryption and retention controls; audit records use digests and references.

# 14. Acceptance and adversarial evidence

This contract cannot become Accepted until a non-production Microsoft 365 tenant demonstrates:

- organisation-only sign-in, PKCE, refresh rotation and disconnect;
- wrong-tenant, consumer, shared-mailbox and revoked-consent rejection;
- exact effective scopes with no application permissions;
- sendMail `202` mapping only to submitted;
- Sent Items match, no-match, ambiguous-match and provider-normalisation behaviour;
- lost-response/timeout classification with no duplicate send;
- each enabled Selected scope, explicit read assignment and Owner-authority intersection;
- source removal, assignment revocation and stale-content denial; and
- suspension races at approval consumption and Graph invocation.

# 15. Open dependencies

- Hosting/platform ADR must provide exact environment origins and redirect URIs.
- Data & Integrations must provide test-tenant evidence for Selected-permission provisioning and reconciliation fields.
- Security must accept the scope, token and adversarial-test evidence.
- Legal must approve token, mailbox evidence, source lineage and retention treatment before live personal data.
- UX must approve customer wording for submitted, sent and indeterminate.

# 16. References

- [Microsoft identity platform authorisation-code flow](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-auth-code-flow)
- [Microsoft Graph delegated access](https://learn.microsoft.com/en-us/graph/auth-v2-user)
- [Microsoft Graph permissions reference](https://learn.microsoft.com/en-us/graph/permissions-reference)
- [Microsoft Graph sendMail](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0)
- [Microsoft Selected permissions overview](https://learn.microsoft.com/en-us/graph/permissions-selected-overview)
