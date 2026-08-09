---
Document title: TeamMates Decision Register
Version: 1.2
Status: Current
Owner: Programme Director / Product-Technology Orchestrator
Last updated: 2026-08-09
---

# 1. Purpose

This register records authoritative TeamMates Product, architecture and trust-control decisions and their change-control status.

Only decisions explicitly approved by the accountable owner are recorded as Active. Recommendations, unresolved findings and pending options are not decisions and must not be implemented as though approved.

# 2. Decision Status

| Status | Meaning |
|---|---|
| Proposed | An accountable owner has issued a proposal, but it is not approved. |
| Active | The decision is approved and binding. |
| Superseded | A newer explicitly approved decision replaces it. |
| Withdrawn | The owner has withdrawn the decision without replacement. |

# 3. Active Decisions

## P-001 — First Commercial TeamMate

| Field | Record |
|---|---|
| Status | Active |
| Decision type | Product |
| Accountable owner | Product Manager |
| Recorded date | 2026-08-08 |
| Effective baseline | SME v1 |
| Decision | The first commercial TeamMate for the UK SME v1 MVP is Admin TeamMate. PM TeamMate and all other specialist TeamMates are outside the v1 baseline. Future-role examples do not authorise implementation. |
| Rationale | A single-role Admin TeamMate MVP provides a coherent proposition, bounded implementation and shorter SME route to value. |
| Primary affected documents | `docs/strategy/product-requirements.md`; `docs/product/admin-teammate-role-handbook.md`; all architecture, UX, engineering, security, commercial and test documents that define v1 scope. |
| Change control | A change requires an explicit Product decision, full downstream impact review and updated requirements/test traceability. |

## D-001 — Deployed TeamMate Lifecycle

| Field | Record |
|---|---|
| Status | Active |
| Decision type | Product behaviour and domain semantics |
| Accountable owner | Product Manager |
| Recorded date | 2026-08-08 |
| Effective baseline | SME v1 |
| Decision | The deployed TeamMate lifecycle is exactly Configuring → Probation → Active → Suspended → Archived. There is no Draft state for a deployed TeamMate. Customer-facing Paused maps to `status = suspended` and `suspension_reason = customer_paused`. Paused is not a separate lifecycle state. |
| Rationale | One canonical lifecycle prevents divergent Product, UX, API, Data and runtime behaviour while preserving customer-friendly Paused language. |
| Primary affected documents | Product Requirements; Admin TeamMate Role Handbook; TMOS Domain Model; Platform/System Architecture; Interaction Model; Security; Data Model; API Contract; UX; onboarding; workflows; tests. |
| Change control | A semantic change requires an explicit Product decision. A material enforcement or persistence change also requires Architecture review and, where material, an ADR. Security and QA must review affected trust controls and tests. |

## PD-001 to PD-007 — SME v1 Product Decision Pack

| Field | Record |
|---|---|
| Status | Active |
| Decision type | Product scope and behaviour |
| Accountable owner | Product Manager |
| Recorded date | 2026-08-09 |
| Effective baseline | SME v1 |
| Decision | The complete, binding wording of PD-001 through PD-007 is recorded in the [Approved Product Decision Pack](product-decision-pack.md). It establishes the bounded human operating model, supervised Probation, distinct lifecycle-adjacent operations, deterministic Work Queue and Today projections, email-only controlled provider write, outcome-based activation evidence and restricted private-beta boundary. |
| Change control | Any Product behaviour change requires an explicit Product decision and downstream Architecture, UX, Security, Data/API, Testing and Commercial impact review. |

## ATC-001 to ATC-008 — Architecture and Trust-Control Decision Pack

| Field | Record |
|---|---|
| Status | Active |
| Decision type | Architecture, security and integration controls |
| Accountable owners | Head of Software / Solution Architect; Security & Governance Lead; Data & Integrations Lead |
| Recorded date | 2026-08-09 |
| Effective baseline | SME v1 |
| Decision | The complete, binding wording of ATC-001 through ATC-008 is recorded in the [Approved Architecture and Trust-Control Decision Pack](architecture-trust-control-decision-pack.md). It establishes deterministic tenant authority, lifecycle enforcement and suspension fencing, payload-bound approval, conservative email reconciliation, delegated Microsoft access, selected-source ACL controls, and transactional audit reconstruction. |
| Change control | Material architecture changes require an ADR. Trust controls cannot be weakened without explicit Security review. Microsoft access changes require Data & Integrations review. All changes require updated traceability and tests. |

# 4. Proposed Decisions

| ID | Status | Decision required |
|---|---|---|
| AI-001 | Proposed | Two-plane deterministic authority and model-context precedence contract |

The complete AI-001 wording and reviewed control/test consequences are in the [TMOS Authority and Model-context Precedence Decision Proposal](ai-authority-decision-proposal.md). AI-001 remains non-binding until explicitly approved and recorded as Active.

# 5. Approved Decision Packs

- The [SME v1 Product Decision Pack](product-decision-pack.md) records PD-001 through PD-007 as Active.
- The [SME v1 Architecture and Trust-Control Decision Pack](architecture-trust-control-decision-pack.md) records ATC-001 through ATC-008 as Active. Approval authorises only the seven ADRs and Microsoft Integration Contract; feature implementation remains subject to evidence and readiness gates.

# 6. Unresolved Decision References

`F-003` is referenced in the reviewed baseline but no canonical record defines its owner, date, decision or supersession rules.

Until the accountable owner supplies evidence, `F-003` is an unresolved reference and has no independent decision authority.

# 7. Supersession Rules

1. Informal conversation, prototype behaviour or implementation detail does not supersede an Active decision.
2. The accountable owner must explicitly state the replacement decision and identify the decision it supersedes.
3. The Orchestrator must record the new decision, affected documents and effective baseline.
4. Material Architecture consequences require an ADR.
5. Security controls may not be weakened without explicit Security review.
6. Requirements and test traceability must be updated before the superseding decision becomes release-ready.

# 8. Related Documents

- [Programme Baseline Audit Report](programme-baseline-audit-report.md)
- [Programme Baseline Audit Brief](programme-baseline-audit-brief.md)
- [Canonical Document Register](../README.md)
- [SME v1 Architecture and Trust-Control Decision Pack](architecture-trust-control-decision-pack.md)
