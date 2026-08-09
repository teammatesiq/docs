---
Title: ADR-011 Tenant Context, RLS and Trusted Worker Envelope
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Security & Governance Lead
Implements: ATC-001, ATC-008
---

# Context

TMOS is multi-tenant. Customer requests, scheduled jobs and asynchronous workers must all resolve the same authoritative Organisation boundary. A client-supplied Organisation identifier, model output or queue payload cannot be trusted as authority.

# Decision

1. The authenticated TMOS session resolves the Owner and exactly one `organisation_id` server-side. Route and payload tenant identifiers are selectors only and must match that context.
2. Every tenant business table contains `organisation_id` directly unless an accepted schema exception proves an equally strong database-enforced ownership chain.
3. PostgreSQL row-level security (RLS) is enabled on tenant business tables as defence in depth. Application authorisation remains mandatory.
4. Each transaction sets tenant context with a transaction-local database setting. Connections return to the pool with no durable tenant context.
5. Ordinary application and worker database roles cannot bypass RLS. Migration and break-glass roles are separate, unavailable to runtime code and audited.
6. Cross-tenant foreign keys use composite tenant-aware keys or equivalent constraints so a valid foreign identifier from another Organisation cannot be attached.
7. Workers accept only a signed, versioned execution envelope containing `organisation_id`, actor/service identity, TeamMate, workflow/action, `control_epoch`, correlation, causation, issued-at, expiry and nonce.
8. The worker resolves the referenced records from PostgreSQL and compares every authority field. Missing, expired, replayed, mismatched or unverifiable envelopes fail closed before material work.
9. The model and frontend cannot invoke a provider adapter. Only an authorised TMOS application service may issue a connector command after deterministic checks.

# Trusted worker envelope

The envelope is a transport assertion, not the source of truth. It must be authenticated with a rotated service key or workload identity, have a short bounded lifetime, and include a unique nonce or message identifier used for replay protection. Queue redelivery is supported through the business idempotency key, not by trusting the envelope twice.

# Tenant table control classes

| Class | Examples | Required controls |
|---|---|---|
| Direct tenant state | TeamMates, workflows, tasks, approvals, connections, sources, attempts | Direct `organisation_id`, RLS, tenant-aware unique and foreign-key constraints |
| Shared immutable catalogue | released role definitions, public capability definitions | No customer mutation; versioned references; no customer data |
| Operational evidence | outbox, inbox/deduplication, audit metadata | Direct `organisation_id`, append-only or state-machine rules, RLS |

# Consequences

- Background processing requires explicit tenant bootstrap and cannot use an unrestricted service role.
- Schema migrations must enumerate every tenant table and its RLS policy.
- Support access is not enabled by this ADR and requires a separate accepted ADR.

# Acceptance evidence

- Tenant-table/RLS matrix and migration tests.
- Cross-tenant read, write, foreign-key and worker-envelope negative tests.
- Pool-reuse test proving transaction-local tenant context cannot leak.
- Replay, expiry, signature and stale-control-epoch tests.
- Dependency test proving model/frontend modules cannot call provider adapters.

