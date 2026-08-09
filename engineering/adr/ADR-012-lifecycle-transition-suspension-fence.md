---
Title: ADR-012 Lifecycle Transition Service and Suspension Fence
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Security & Governance Lead
Implements: D-001, PD-002, PD-003, ATC-002, ATC-003
---

# Context

The deployed lifecycle is exactly Configuring, Probation, Active, Suspended and Archived. “Paused” is a projection of `suspended/customer_paused`. State checks at workflow creation alone cannot stop already queued or claimed work.

# Decision

1. A single lifecycle domain service owns transitions. Repositories expose no general-purpose status setter.
2. Each TeamMate stores `status`, `lifecycle_version`, `control_epoch`, transition timestamps and `suspended_from_status`.
3. Transitions use optimistic concurrency against `lifecycle_version`; success records state and an immutable audit/outbox event in one transaction.
4. Suspension atomically increments `control_epoch`, records an active suspension cause, stops new scheduling and fences non-started work.
5. Runtime checks current lifecycle and epoch before queue publication, worker claim, material model execution, artefact publication, approval creation, approval consumption and connector invocation.
6. Results produced under a stale epoch are discarded or quarantined and never become customer-visible or externally effective.
7. All approvals from an earlier epoch become stale permanently, including after reactivation.
8. Reactivation is permitted only after every blocking cause is cleared and identity, entitlement, Microsoft connection, permissions, policy, configuration and source authority revalidate.
9. Reactivation returns to `suspended_from_status`. Active cannot return to Probation in SME v1.
10. Archive first applies the suspension fence, completes the approved offboarding transaction and enters terminal Archived. Archived never reactivates.

# Transition table

| From | To | Preconditions |
|---|---|---|
| Configuring | Probation | PD-006 activation criteria and all required controls pass |
| Probation | Active | PD-006 probation-exit evidence passes |
| Configuring, Probation, Active | Suspended | Any valid suspension cause; immediate fence |
| Suspended | prior recorded state | All causes cleared and controls revalidated |
| Configuring, Probation, Active, Suspended | Archived | Authorised offboarding and suspension fence complete |

No other transition is valid.

# Capability matrix

| State | Customer work | Approved email send |
|---|---|---|
| Configuring | Setup and safe validation only | No |
| Probation | Authorised read, analysis and preparation | Yes, under ADR-013 and ADR-014 |
| Active | Same catalogue as Probation | Yes, under ADR-013 and ADR-014 |
| Suspended | None | No |
| Archived | None | No |

Suspension-cause precedence affects presentation only: security, admin, integration disconnect, subscription, trial expiry, customer pause. Every cause remains independently auditable and must be cleared.

# Consequences

- Pausing cannot recall a provider request already submitted; ADR-014 reconciliation continues as platform-only activity.
- Queue technology remains undecided, but it must support the lease, epoch and idempotency contract.

# Acceptance evidence

- Database constraints and complete transition tests.
- Approve-versus-pause, send-versus-pause and archive race tests.
- Stale-epoch tests at every boundary and Archive irreversibility proof.

