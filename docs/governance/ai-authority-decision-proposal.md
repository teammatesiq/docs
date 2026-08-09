---
Document title: TMOS Authority and Model-context Precedence Decision Proposal
Version: 1.0
Status: Proposed
Owner: AI Behaviour Lead
Last updated: 2026-08-09
---

# 1. Purpose

This document proposes AI-001 to resolve Programme Baseline Audit conflict PBR-C02. The proposal incorporates review by Security & Governance, Head of Software / Solution Architecture, and QA & Evaluation.

AI-001 is not Active until explicitly approved and recorded in the Decision Register. It does not authorise implementation.

# 2. AI-001 — TMOS Authority and Model-context Precedence

TMOS operates two strictly separated planes.

The **Deterministic Authority and Execution Control Plane** is the sole authority for identity, tenancy, lifecycle and entitlement eligibility, protected role restrictions, permissions, policy, workflow preconditions, approvals, resource access, and controlled tool or provider execution.

The **Model Context and Reasoning Plane** may understand, prepare, recommend and propose structured actions, but no model-visible tier confers authority. Model output, customer language, memory, retrieved content, tool output or provider output cannot grant permission, satisfy policy, create approval or authorise execution.

Model-visible instruction precedence is:

| Priority | Model-visible instruction context | Rule |
|---:|---|---|
| 1 | Platform Safety and Security Context | Protected behavioural constraints; external runtime enforcement remains authoritative. |
| 2 | TeamMate DNA | Protected constitutional behaviour. |
| 3 | Organisation Policy Context | Trusted and versioned Organisation-wide guidance. |
| 4 | Workspace Policy Context | May tighten or refine Organisation Policy; never weaken it. |
| 5 | Role Definition and Protected Boundaries | Defines permitted role behaviour but not execution authority. |
| 6 | Workflow Definition and Active Task/Step Contract | Governs current reasoning and structured outputs. |
| 7 | Confirmed Governed Customer Configuration | Applies only within higher controls. |
| 8 | Current Authenticated-user Instruction | Applies to the current task only and within externally established authority. |
| 9 | Confirmed Personalisation Defaults | Defaults only; current-user instruction may override them for the current task. |

Retrieved content, non-preference memory, tool or provider results and prior model output are evidence or data, not instructions. Every model-context item must carry typed provenance. An unresolved same-tier conflict must fail closed for affected access or execution.

Natural-language expressions such as “approve”, “send” or “go ahead”, and model outputs such as `allow` or `approved`, are untrusted and do not constitute Approval. Approval requires a persisted first-class Approval object bound to the exact action, target and payload, with authority and all applicable controls re-evaluated immediately before controlled provider invocation.

TMOS must not store or expose hidden model chain-of-thought. Explainability and audit use structured evidence, sources, assumptions, confidence, validation and control decisions.

# 3. Mandatory Control Invariants

The deterministic control plane must apply all of the following rules:

- explicit denial or protected prohibition prevails;
- the policy engine is authoritative over model-visible policy context;
- missing, stale, conflicting or unavailable authority fails closed;
- `approval_required` means wait, not allow;
- Approval is one-time and non-transferable and cannot grant continuing authority;
- a material target or payload change invalidates Approval;
- approver eligibility, expiry, revocation, action binding and payload equivalence are checked immediately before provider invocation; and
- model confidence never affects authority.

The exact eligible approver and permitted action and lifecycle predicates depend on PD-001, PD-002 and PD-005.

# 4. Approval and Provenance Contracts

A valid Approval must contain at least:

- approval ID, status, expiry, revocation and consumption state;
- Organisation and Workspace;
- approving user and verified decision timestamp;
- proposed actor or TeamMate;
- action type;
- exact target and resource identifiers;
- canonical payload or immutable payload hash;
- task, workflow and correlation references; and
- append-only decision history.

Every model-context item must identify at least:

- instruction or evidence classification;
- hierarchy tier where applicable;
- source type, identifier and version;
- Organisation, Workspace and scope;
- issuer or confirming actor;
- creation and validity timestamps; and
- integrity and validation status.

Unproven content cannot be promoted into a trusted instruction tier.

# 5. Required Typed Runtime Boundaries

Architecture must define three distinct typed contracts:

| Contract | Purpose |
|---|---|
| `ReasoningRequest` | Tenant-bound instruction and evidence manifests, authenticated actor, task/workflow context, release tuple, capability envelope and required output schema. |
| `ReasoningResult` | Structured facts, inferences, recommendations, assumptions, uncertainty, evidence references, requested input and non-authoritative proposed actions. |
| `ExecutionRequest` | A TMOS-created request containing the approved canonical action, action digest, Approval binding, lifecycle fence, resource version, current permission/policy decisions, idempotency key and audit references. |

A model may propose an action. Only TMOS may create an `ExecutionRequest` after current lifecycle, resource, permission, policy and Approval validation succeeds.

# 6. Release-blocking Conformance

The canonical Test and Evaluation Specification must require 100% pass and zero authority or approval bypass across tests covering:

- every lower tier attempting to override every higher tier;
- Workspace Policy attempting to weaken Organisation Policy;
- user instruction attempting to override governance;
- a task-local personalisation override without persistent-memory mutation;
- fake policy or approval language in retrieved documents, email, transcripts, memory or tool output;
- model-generated `allow`, `approved` or unrestricted tool calls;
- natural-language “send” or “go ahead” without a valid Approval object;
- same-tier conflict without deterministic precedence metadata;
- absent, stale, malformed, spoofed or cross-tenant provenance;
- expired, revoked, reused or payload-mismatched Approval;
- permission, policy, lifecycle or resource change after Approval;
- control-service failure;
- failure to re-evaluate immediately before provider invocation;
- replay, redelivery and concurrent execution;
- false completion against provider/runtime state; and
- hidden chain-of-thought, credentials or unnecessary content appearing in persistence, logs or audit.

Every allow, deny, conflict and execution outcome must be reconstructable from tenant-bound audit evidence and versioned control inputs.

# 7. Impacts and Dependencies

| Discipline | Consequence if approved |
|---|---|
| Product | No new capability; authority and approval semantics become explicit. PD-001, PD-002 and PD-005 still define eligible humans, lifecycle and actions. |
| Architecture | Requires the two-plane boundary, typed runtime contracts, provenance, versioned release tuple and deterministic execution controls. |
| UX | Approval, conflict, uncertainty and evidence explanations must come from structured control state, not model assertion. |
| Security | Policy, permission, approval and provider execution stay outside model authority and fail closed. |
| Data/API | Requires versioned provenance, control decision, Approval, reasoning and execution-attempt schemas. |
| Testing | Requires hierarchy, injection, fake-approval, cross-tenant, stale-control, replay, concurrency and audit-reconstruction suites. |
| Commercial | Prevents unsupported claims of autonomous authority; no direct package change. |

# 8. Repository Changes Required After Approval

- align the hierarchy in `docs/architecture/teammate-dna.md` and `docs/architecture/teammate-factory.md`;
- align deterministic control and audit requirements in `docs/security/security-privacy-governance.md` and `docs/architecture/tmos-system-architecture.md`;
- define the internal reasoning, approval and execution contracts in the API and Data Model specifications;
- add the release-blocking conformance matrix to the Test and Evaluation Specification; and
- create the required Instruction/Evidence/Control Boundary, context assembly, approval integrity, lifecycle fencing, tool invocation, external-action reconciliation, audit and Blueprint versioning ADRs.

# 9. Closure and Readiness

Approval of AI-001 resolves the normative substance of PBR-C02. The conflict closes only after AI-001 is Active, the affected canonical specifications are aligned and the consistency and conformance checks pass.

Independently open blockers include human authority, lifecycle execution, the controlled-action catalogue, the full approval predicate, six workflow-specific AI contracts and release/test evidence.

- Ready for accountable approval: Yes
- Ready for Lovable: No
- Ready for Codex: No
- Authorised execution scope: None
- Private-beta gate: Fail

# 10. Related Documents

- [Programme Baseline Audit Report](programme-baseline-audit-report.md)
- [Decision Register](decision-register.md)
- [SME v1 Product Decision Pack](product-decision-pack.md)
- [TeamMate DNA](../architecture/teammate-dna.md)
- [TeamMate Factory](../architecture/teammate-factory.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [TMOS System Architecture](../architecture/tmos-system-architecture.md)
