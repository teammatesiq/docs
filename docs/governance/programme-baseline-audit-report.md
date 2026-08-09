---
Document title: TeamMates Programme Baseline Audit Report
Version: 1.0
Status: Draft
Owner: Programme Director / Product-Technology Orchestrator
Last updated: 2026-08-09
---

# 1. Purpose

This report reconciles the specialist reviews conducted under the TeamMates Programme Baseline Audit Brief.

It determines whether the SME v1 specification set enables Product, UX, Architecture, Security, AI Behaviour, Data, Engineering, QA, Platform, Commercial, Customer Success and Legal to implement and operate the same Admin TeamMate product without making material assumptions.

This report records review evidence, conflicts, blockers, decision ownership and the required closure sequence. It does not approve unresolved Product behaviour, Architecture choices, Security controls, commercial terms or legal conclusions.

# 2. Audit Basis

- repository: `teammatesiq/docs`
- branch: `main`
- reviewed commit: `9846ba96217e1a6db64df013c2f66904fde22adb`
- commit description: `Reconcile TeamMates v1 canonical specification register`
- review date: 2026-08-09
- specialist reviews completed: 11 of 11

The Orchestrator verified after the reviews that the latest `main` commit remained the reviewed commit.

The local Programme Baseline Audit Brief and this report are governance overlays created after that commit. They do not alter the product baseline under review.

# 3. Review Panel

The following specialist owners completed evidence-based reviews:

1. Product Manager
2. Head of Software / Solution Architect
3. UX & CX Lead
4. Security & Governance Lead
5. AI Behaviour Lead
6. QA & Evaluation Lead
7. Platform, DevOps & Reliability Lead
8. Data & Integrations Lead
9. Customer Implementation & Success Lead
10. Legal, Privacy & Compliance Lead
11. Commercial Lead

Each review was restricted to the specialist's delegated authority. Specialists did not edit the baseline during review.

# 4. Programme Verdict

## DECISION / RECOMMENDATION

Do not authorise Lovable or Codex implementation against the reviewed baseline.

The baseline contains strong product, trust and architecture direction, but it is not deterministic enough for two competent teams to build materially the same v1 product. It also lacks the acceptance, operating and legal evidence required for a controlled private beta.

The specialist findings reconcile to:

- 14 consolidated Blockers
- 10 consolidated High-risk themes
- 8 explicit cross-document conflicts or authority ambiguities
- 0 known Critical findings identified from specification review

The absence of a known Critical finding is not evidence that no Critical defect exists. The required security, adversarial, tenant-isolation, approval-integrity and duplicate-execution suites have not yet been defined or executed.

## EXECUTION READINESS

- Ready for Lovable: No
- Ready for Codex: No
- Authorised execution scope: None
- Decision required first: Yes
- Private-beta gate: Fail

# 5. Binding Decision Validation

All 11 specialist leads independently validated the following decisions.

## P-001 — First Commercial TeamMate

The first commercial TeamMate for the UK SME v1 MVP is Admin TeamMate.

PM TeamMate and all other specialist TeamMates remain outside the v1 baseline. Future-role examples do not authorise implementation.

## D-001 — Deployed TeamMate Lifecycle

The deployed lifecycle is exactly:

Configuring → Probation → Active → Suspended → Archived

There is no Draft lifecycle state for a deployed TeamMate.

Customer-facing Paused maps to:

- `status = suspended`
- `suspension_reason = customer_paused`

Paused is not a separate lifecycle state.

The state vocabulary is consistent. The complete transition, guard, concurrency and recovery contract is not.

# 6. Consolidated Blocker Register

The register deduplicates overlapping specialist findings. Closure of one blocker may require several specialist artefacts.

| ID | Blocker | Evidence and consequence | Decision owner | Closure evidence |
|---|---|---|---|---|
| PBR-B01 | Canonical workflow and onboarding/probation behaviour is absent | `docs/product/admin-teammate-workflows.md` and `docs/product/admin-teammate-onboarding-probation.md` are placeholders. Happy-path fragments do not define triggers, actors, states, approvals, exceptions, failure, recovery or acceptance. | Product Manager | Approved substantive specifications for all six workflows and onboarding/probation, with controlled references, threat treatment and QA traceability. |
| PBR-B02 | The v1 human operating model and authority matrix is undefined | Product, Security, API and Data sources use `customer`, `user`, `authorised human` and suggested roles without deciding single-user versus multi-user behaviour or governed action authority. | Product Manager; Security review | Recorded Product decision and security-reviewed matrix for organisation, invitations, deployment, configuration, connections, approvals, pause, reactivation, disconnect and archive. |
| PBR-B03 | Lifecycle transition semantics and Probation execution conflict | Product requires successful live-business workflows during Probation, while System Architecture requires `active` before execution. Guards, failure, extension, suspension origins, recovery, archive and in-flight work are incomplete. | Product Manager; Head of Software | Product transition matrix plus deterministic lifecycle and suspension-fencing contract, aligned across Architecture, API, Data, UX and tests. |
| PBR-B04 | Pause, integration disconnect, source disconnect, TeamMate offboarding and archive are conflated | FR-030 and the Role Handbook promise disconnection of Admin TeamMate, while API and Security define integration/source disconnect and D-001 has no disconnected TeamMate state. | Product Manager | Explicit semantics, authority, reversibility, data treatment, token revocation, workflow effects, audit and customer terminology for every operation. |
| PBR-B05 | The authoritative UX information architecture, journeys and interface states are absent | `docs/ux/admin-teammate-ux-ui-specification.md` is a placeholder. Primary surfaces, navigation, loading, empty, partial, failure, stale, retry, suspended, archived and disconnected experiences are not testable. | UX & CX Lead after Product and Security decisions | Approved end-to-end UX specification with route, surface, state, responsive and acceptance contracts. |
| PBR-B06 | Work Queue classification is non-deterministic | Four customer groups exist, but task, workflow, approval and integration states have no authoritative mapping or precedence rule. | Product Manager; UX & CX Lead | Versioned state-to-group mapping, projection/API contract, worked examples and QA cases. |
| PBR-B07 | Release, test, traceability and evidence governance is absent | The Engineering Release Plan and Test/Evaluation Specification are placeholders; no requirements-to-test matrix, gate evidence, environment model or exception authority exists. | Head of Software; QA & Evaluation Lead | Approved dependency-ordered release plan, test/evaluation specification, traceability matrix, evidence model and measurable gates. |
| PBR-B08 | API and database drafts cannot produce deterministic OpenAPI or migrations | Contracts contain conceptual, suggested and optional structures; exact schemas, status codes, authority, constraints, RLS policies, state preconditions and migration order are incomplete. | Head of Software; Data & Integrations Lead | Reviewed OpenAPI subset, closed schema contract, migrations and contract/migration tests after upstream decisions. |
| PBR-B09 | Blueprint and deployed-role version persistence is unresolved | Factory and API require a versioned Blueprint, while the data model has no canonical Blueprint entity and uses a free `blueprint_version` field. | Head of Software / Solution Architect | Accepted Blueprint/Role persistence ADR and aligned Factory, Domain, API and Data specifications. |
| PBR-B10 | Microsoft identity, Graph permission, consent and synchronisation contract is absent | Delegated versus application/hybrid access, exact scopes, mailbox/source boundaries, consent authority, webhooks, delta sync, throttling, revocation, ACL preservation and recovery are unspecified. | Data & Integrations Lead; Product, Architecture, Security and Legal decisions | Approved Microsoft Integration Contract, ADRs, scope/resource matrix, consent and sync state machines, schema/API changes and release-blocking tests. |
| PBR-B11 | AI protected instruction hierarchy is contradictory | TeamMate DNA places Organisation Policy above Role and includes Permissions; TeamMate Factory places Role above Policy and omits Permissions. | AI Behaviour Lead; Security and Architecture review | One normative hierarchy that separates model instruction precedence from deterministic permission and policy enforcement, with adversarial conformance tests. |
| PBR-B12 | Workflow-specific AI contracts and evaluation evidence are absent | The workflow and test placeholders prevent deterministic grounding, structured output, uncertainty, prohibited-action, fallback, golden, safety and regression behaviour. | AI Behaviour Lead; Product and QA dependencies | Six workflow AI contracts, canonical output schemas, versioned datasets/rubrics, thresholds and passing evaluation for the exact release tuple. |
| PBR-B13 | External-action completion and duplicate-prevention semantics are unsafe to infer | The baseline depicts Microsoft email as `Confirmed`, but Graph acceptance is not delivery completion. Draft ownership, indeterminate outcomes, reconciliation and safe retry are undefined. | Product Manager; Head of Software | Approved prepared/submitted/sent/delivered semantics, draft system of record, persisted attempt/reconciliation model and duplicate-prevention tests. |
| PBR-B14 | Commercial package, trial, entitlement and billing behaviour is not approved | `docs/strategy/product-commercial-strategy.md` is a placeholder while Product, Architecture, API and Data assume trial, subscription and entitlement behaviour. | Commercial Lead; Product and Architecture review | Approved Commercial Strategy and decision record aligned to lifecycle, onboarding, UX, entitlement, billing, metrics, legal terms and tests. |

# 7. Consolidated High-Risk Themes

These themes prohibit private beta until closed or formally treated by the authorised owner.

| ID | High-risk theme | Primary owner | Required outcome |
|---|---|---|---|
| PBR-H01 | Tenant context, table ownership, RLS, service-role and worker-path isolation | Head of Software; Security review | Tenancy/RLS ADR, table/control matrix, migrations and negative cross-tenant tests. |
| PBR-H02 | Controlled-action registry, approver eligibility, stale approval, payload equivalence and approval concurrency | Security & Governance; Product catalogue | Approved action/control matrix, ADR, immutable binding and bypass/mutation tests. |
| PBR-H03 | Knowledge-source ACL preservation, freshness, revocation and derived-work lineage | Data & Integrations; Security and Architecture review | ACL/lineage model and same-tenant cross-user, group-change, stale-authority and reconstruction tests. |
| PBR-H04 | AI output schema, evidence semantics, asset versioning, provider/model selection and rollback | AI Behaviour; Architecture; QA | Immutable release tuple, provider ADR and regression/promotion policy. |
| PBR-H05 | Trust presentation, accessibility and responsive acceptance | UX & CX; Security and QA review | Explainability patterns, WCAG 2.2 AA scope, responsive matrix and comprehension evidence. |
| PBR-H06 | Hosting, environments, CI/CD, secrets, queue, storage, observability, SLO, RTO/RPO and disaster recovery | Platform; Architecture and Security review | Platform operability specification, accepted ADRs, monitored staging, restore/DR evidence and exercised runbooks. |
| PBR-H07 | Customer activation, Probation operations, support, manual intervention, health, value and beta protocol | Customer Implementation & Success | Approved operating model, support-readiness plan, measurement specification and rehearsed beta protocol. |
| PBR-H08 | UK GDPR roles, DPIA, DPA, transparency, subprocessors/transfers, retention, rights, breach and support access | Legal; factual owners and external counsel | Complete legal evidence package before any live-personal-data beta. |
| PBR-H09 | Trial/entitlement state mapping, provider reconciliation, commercial events, claims and gross-margin evidence | Commercial; Product, Architecture, Data, Legal and QA | Approved commercial decisions, state mapping, event catalogue, claims register and tested billing reconciliation. |
| PBR-H10 | Audit reconstruction, mandatory evidence attributes and retention | Architecture; Security, Data and Legal review | Normative audit/event schema, append-only enforcement, retention rules and reconstruction tests. |

# 8. Explicit Conflicts and Ambiguities

Conflicts must not be closed by blending incompatible wording.

## PBR-C01 — Execution during Probation

- Product sources require useful supervised work and successful core workflows during Probation.
- System Architecture requires `active` before active execution.
- Owner: Product Manager for permitted behaviour; Head of Software for enforcement.

## PBR-C02 — AI authority hierarchy

- TeamMate DNA orders Organisation Policy above Role Definition and includes Permissions.
- TeamMate Factory orders Role above Policy and omits Permissions.
- Owner: AI Behaviour Lead, with Security and Architecture approval.
- A reviewed [AI-001 decision proposal](ai-authority-decision-proposal.md) is ready for approval; the conflict remains open until it is Active and the affected specifications and tests are aligned.

## PBR-C03 — Future multi-TeamMate hand-offs in v1 Definition of Done

- The PRD excludes multi-TeamMate collaboration.
- The Interaction Model labels hand-offs as future but includes structured hand-offs in its Definition of Done.
- Owner: Product Manager.

## PBR-C04 — Calendar write and external document action scope

- The PRD requires calendar reading.
- Other Product sources contemplate creating or modifying meetings, provider files and human work assignments.
- Owner: Product Manager.

## PBR-C05 — Subscription release ordering

- Deployment validation assumes entitlement in an early release.
- Subscription endpoints are provisionally deferred to a later release.
- The commercial strategy and engineering release plan are placeholders.
- Owner: Head of Software after Commercial and Product decisions.

## PBR-C06 — Visible value estimate

- The PRD requires a visible estimate of work/value.
- The Role Handbook makes time-saved estimation optional and excludes it from its beta Definition of Done.
- Owner: Product Manager.

## PBR-C07 — External email `Confirmed`

- Architecture/API examples imply a confirmed Microsoft outcome.
- Provider acceptance does not itself establish delivery completion.
- Owner: Product Manager for customer semantics; Head of Software for reconciliation.

## PBR-C08 — Organisation, Subscription and TeamMate states

- The data model defines overlapping Organisation, Subscription and TeamMate status models without an authoritative mapping.
- D-001 must not be inferred directly from billing-provider or Organisation status.
- Owner: Product Manager and Head of Software.

# 9. Pending Decision Agenda

These are pending decisions, not approved requirements.

## Product decisions — required first

| ID | Decision | Required reviewers |
|---|---|---|
| PD-001 | Single-user versus multi-user v1 and the human authority matrix | Security, UX, Data/API, QA, Commercial |
| PD-002 | Complete lifecycle transition matrix, execution permitted in Probation, suspension origins, failure, extension, re-entry, recovery and archive | Architecture, Security, UX, Data/API, QA, Customer Success, Commercial |
| PD-003 | Distinct semantics for Pause, TeamMate offboarding, TeamMate Archive, integration disconnect, source disconnect and organisation termination | Architecture, UX, Security, Data, Legal, Customer Success, Commercial |
| PD-004 | Authoritative Work Queue projection and whether Today is broader than the Daily Briefing | UX, Architecture, Data/API, QA |
| PD-005 | Calendar write, Outlook versus TMOS drafts, document write/share, human work assignment and other controlled v1 actions | Architecture, Security, Data, UX, AI, QA |
| PD-006 | Activation point, core Probation workflows, first-value definition and beta metric classification | Customer Success, QA, Data, UX, Commercial |
| PD-007 | Customer and data eligibility: supported Microsoft accounts/mailboxes, sensitive-data/sector exclusions and live-data beta boundary | Data, Security, Legal, Commercial, Customer Success |

## Commercial decision — required before trial or checkout work

The Commercial Lead recommends, subject to approval and legal review:

- one Admin TeamMate package;
- one Organisation subscription entitling one deployed Admin TeamMate;
- £299 per month excluding VAT where applicable;
- monthly billing in advance;
- one 14-calendar-day Organisation trial without a payment card;
- no annual plan, add-ons, discounts or customer-facing usage pricing in v1;
- no customer-facing SLA until measured evidence and an explicit commitment exist.

This is a recommendation, not an approved decision.

## Architecture and control decisions

ADR numbering and grouping remain owned by the Head of Software. The accepted set must cover, at minimum:

- modular monolith, persistence, events/outbox and no per-TeamMate infrastructure;
- application stack, repository topology, module dependencies and transaction ownership;
- human identity, tenant context and RLS;
- Blueprint/Role persistence and lifecycle enforcement;
- Microsoft OAuth/access mode, sync/webhooks, ACL preservation and external-action reconciliation;
- hosting, environment topology, compute, database, queue, object storage, secrets, observability, network and disaster recovery;
- AI provider/model, release tuple and rollback;
- approval integrity and controlled-action execution;
- billing provider and entitlement boundary;
- production support access.

## Legal and factual decisions

Before live personal data, confirm:

- the TeamMates contracting legal entity and privacy contact;
- ICO fee and DPO assessments;
- named providers, contracting entities, processing/support locations and transfer mechanisms;
- whether customer content is ever used for TeamMates or provider training/improvement;
- final controller/processor roles, lawful bases and special-category/offence-data treatment;
- statutory/entity-specific retention and contract terms through external UK counsel.

# 10. Required Closure Sequence

1. Record P-001 and D-001 in the canonical decision register.
2. Resolve PD-001 through PD-007 under Product authority.
3. Approve the Commercial package/trial/entitlement decision.
4. Complete the canonical Workflow and Onboarding/Probation specifications.
5. Resolve the AI instruction hierarchy and workflow-specific reasoning contract.
6. Approve the Microsoft Integration Contract and the initial dependency-gated ADR set.
7. Complete Security threat/control contracts, the UX specification and the Commercial Strategy.
8. Complete the Legal, Platform and Customer Success operating/evidence specifications required for controlled beta.
9. Complete the API, Data, Engineering Release and Test/Evaluation specifications.
10. Create requirements traceability, accepted ADRs, OpenAPI and migrations for the first approved release slice.
11. Re-run consistency, link, authority, lifecycle and traceability checks.
12. Close all Critical and Blocker findings and treat every High finding through its authorised owner.
13. Create the baseline manifest against exact approved document versions and commit.
14. Issue one precise Codex or Lovable implementation prompt for the first approved slice.

# 11. Downstream Impacts

## Product

Admin TeamMate and the fixed lifecycle vocabulary are stable. Executable workflow, authority, transition, disconnect, Work Queue, controlled-action and success semantics are not.

## Architecture

The logical direction is viable, but executable boundaries, required ADRs, lifecycle, Blueprint persistence, tenancy, provider and transaction contracts are incomplete.

## UX

End-to-end journeys, information architecture, system states, trust presentation, responsive rules and accessibility acceptance are not implementation-ready.

## Security

Core principles are strong. Exact human authority, RLS, approval integrity, suspension fencing, OAuth, source ACL, support access, threat treatment and evidence are incomplete.

## Data/API

Microsoft, lifecycle, Work Queue, lineage, ACL and external-action contracts are not sufficient for deterministic OpenAPI or migrations.

## Testing

No approved strategy, traceability, test catalogue, environments, thresholds, evidence store or release-quality gate exists.

## Commercial

One concrete package/pricing recommendation now exists, but no price, promise, trial, entitlement, term or claim is canonical.

# 12. Repository Changes Required

This report does not authorise specialists to implement their proposed changes before the required decisions are recorded.

The authoritative owners must create or update the files identified in the specialist reviews. The minimum programme-control changes are:

- `docs/governance/decision-register.md`
- this Programme Baseline Audit Report
- completed canonical specifications
- accepted ADRs
- requirements traceability matrix
- legal, platform and customer-operating evidence specifications
- baseline manifest after exit criteria pass

# 13. Current Execution Readiness

## DECISION / RECOMMENDATION

Proceed to owner-led decision closure. Do not issue a Lovable or Codex implementation prompt yet.

## DEPENDENCIES / QUESTIONS

The [SME v1 Product Decision Pack](product-decision-pack.md) is ready for accountable approval of PD-001 through PD-007. Architecture impact analysis is complete; the remaining dependent Architecture, Security, Data, AI, Commercial and Legal controls must follow recorded Product decisions.

## EXECUTION READINESS

- Ready for Lovable: No
- Ready for Codex: No
- Authorised execution scope: None
- Decision required first: Yes
- Private-beta gate: Fail
- Critical findings: 0 known from specification review
- Consolidated Blockers: 14
- Consolidated High-risk themes: 10

# 14. Related Documents

- [Programme Baseline Audit Brief](programme-baseline-audit-brief.md)
- [Canonical Document Register](../README.md)
- [Decision Register](decision-register.md)
- [SME v1 Product Decision Pack](product-decision-pack.md)
- [TMOS Authority and Model-context Precedence Proposal](ai-authority-decision-proposal.md)
- [Product Requirements](../strategy/product-requirements.md)
- [TMOS System Architecture](../architecture/tmos-system-architecture.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [API Contract and Service Interfaces](../engineering/api-contract-service-interfaces.md)
- [Data Model and Database Schema](../engineering/data-model-database-schema.md)
