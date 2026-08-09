---
Title: ADR-017 Transactional Outbox, Idempotency and Audit Reconstruction
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Security & Governance Lead
Implements: ATC-008
---

# Context

TMOS must atomically preserve business state and the intent to continue asynchronous processing. Logs cannot prove approval, lifecycle or external-action history, and at-least-once delivery can duplicate effects without explicit idempotency.

# Decision

1. PostgreSQL is authoritative for lifecycle, workflow/task state, approvals, controlled-action attempts, connection/source authority and audit metadata.
2. A state change and its outbox message commit in the same database transaction.
3. Outbox publishers may deliver at least once. Consumers use an inbox/deduplication record plus a unique business idempotency key before applying effects.
4. External effects use a unique controlled-action attempt created before provider invocation. No consumer may create a second provider attempt for the same approval.
5. Audit events are append-only and produced by deterministic TMOS services, not by the model.
6. Each event records Organisation, actor/source, TeamMate/workflow/task/action references, event type, prior/new state where applicable, policy/permission/control versions, correlation/causation IDs, occurred/recorded times and evidence references.
7. Sensitive payloads are stored separately with encryption and access control. Audit metadata retains a digest/reference sufficient for reconstruction.
8. Event schemas are versioned. Consumers tolerate additive change; breaking changes require a new event version and migration/replay plan.
9. Replay may rebuild projections but cannot repeat controlled external actions. Effect-producing consumers check the authoritative attempt state.
10. Retention, legal hold and deletion periods remain Legal decisions; storage must support policy-based enforcement and verifiable deletion.

# Transaction boundaries

| Operation | Atomic records |
|---|---|
| Lifecycle transition | TeamMate version/epoch, suspension causes, audit event, outbox |
| Approval decision | Approval terminal state, audit event, outbox |
| Approval consumption | Consumption marker, action attempt, audit event, outbox |
| Source removal | Source retrieval fence, sync cancellation intent, tombstone, audit event, outbox |

# Consequences

- Queue choice remains open but must support redelivery without relying on exactly-once transport.
- Observability logs may aid diagnosis but cannot replace business/audit records.
- Outbox cleanup cannot occur until publication evidence and retention policy allow it.

# Acceptance evidence

- Crash-before/after-commit and duplicate-delivery tests.
- Append-only audit enforcement and schema-version tests.
- Projection replay test and end-to-end reconstruction of one approved email attempt.
- Proof that replay cannot reinvoke Graph.

