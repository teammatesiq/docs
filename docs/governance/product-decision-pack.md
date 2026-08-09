---
Document title: TeamMates SME v1 Product Decision Pack
Version: 1.0
Status: Approved
Owner: Product Manager
Last updated: 2026-08-09
---

# 1. Purpose

This pack records the approved closure of Product decisions PD-001 through PD-007 identified by the TeamMates Programme Baseline Audit.

PD-001 through PD-007 were explicitly approved and became Active on 2026-08-09. P-001 and D-001 remain Active and unchanged.

# 2. Binding Context

- **P-001:** Admin TeamMate is the first commercial TeamMate for the UK SME v1 MVP. PM TeamMate and all other specialist TeamMates are outside v1.
- **D-001:** The deployed lifecycle uses exactly Configuring, Probation, Active, Suspended and Archived. There is no deployed Draft state. Customer-facing Paused maps to `status = suspended` and `suspension_reason = customer_paused`.

# 3. Active Decisions

## PD-001 — Bounded Multi-user Operating Model

SME v1 supports one Organisation, one default Workspace and the following authenticated human roles:

| Role | Recommended v1 authority |
|---|---|
| Owner | All Admin authorities; transfer ownership; initiate Organisation termination; approve TeamMate Archive. At least one Owner must always remain. |
| Admin | Invite and remove users except the last Owner; deploy and configure Admin TeamMate; manage approved knowledge and customer-controlled permission settings; connect or disconnect an integration where the human has provider authority; pause and reactivate Admin TeamMate. |
| Member | Delegate work, provide input, view and use authorised product surfaces within scope. A Member has no governance authority by default. |

An Owner has all Admin capabilities. Custom roles, multiple Workspaces, teams and cross-Organisation administration are outside v1.

Role membership alone never authorises a controlled external action. Approval eligibility must be checked for the exact action and resource, including current role, tenant, permission, lifecycle and provider authority. A person may not approve an action merely because they are an Owner or Admin.

## PD-002 — Supervised Operational Probation

Probation is a live, supervised operating state. Admin TeamMate may run approved workflows on live eligible data under the Probation control profile. External actions remain subject to the same payload-bound approval and execution controls as Active operation. Entry to Active is never automatic.

| From | To | Recommended product rule |
|---|---|---|
| Configuring | Probation | Required configuration, integration, permission and onboarding checks pass. |
| Probation | Active | Readiness evidence passes and an authorised human confirms exit. |
| Configuring, Probation or Active | Suspended | A customer, entitlement, security, required-integration or authorised administrative control requires execution to stop. |
| Suspended | Recorded prior non-archived state | The suspension cause is resolved and all current controls pass revalidation. |
| Suspended | Archived | Authorised offboarding completes. |
| Archived | Any state | Prohibited. |

Active does not return to Probation in v1. Suspension fences new execution and prevents queued, scheduled or previously approved controlled actions from proceeding. Reactivation revalidates all applicable controls and does not revive stale work automatically. Archive is terminal.

## PD-003 — Distinct Pause, Connection, Source, Offboarding and Termination Operations

| Operation | Recommended meaning and outcome |
|---|---|
| Pause | A reversible lifecycle transition to Suspended with `customer_paused`; it does not disconnect an integration or archive data. |
| Reactivate | Revalidate current controls and return to the recorded prior non-archived state; stale actions do not resume automatically. |
| Disconnect an integration | Revoke or disable that provider connection and stop dependent access. Loss of the required primary Microsoft 365 connection causes a separately audited suspension with reason `required_integration_unavailable`; the customer sees **Connection Issue**. |
| Remove a knowledge source | Stop new retrieval immediately and remove or disable derived retrievable content under the approved retention and deletion contract. Suspend only when the source is required for safe operation. |
| Offboard TeamMate | A guided workflow that fences execution, explains consequences, removes TeamMate-specific access and ends in Archive. Offboarding is not a lifecycle state. |
| Archive TeamMate | The terminal lifecycle transition from Suspended after authorised offboarding. It is not a synonym for Pause. |
| Terminate Organisation | A separate account, entitlement, access and data-handling process governed by contract and law. |

“Disconnect TeamMate” is not a v1 customer operation. Product and UX language must use the distinct operation names above.

## PD-004 — Deterministic Work Queue Projection and Broader Today Surface

The Work Queue is the durable record of work. Each visible item appears in exactly one primary group using the first matching rule below:

| Precedence | Group | Authoritative inclusion rule |
|---:|---|---|
| 1 | Completed | The item has a genuine terminal outcome. Completed, rejected, cancelled and failed outcomes remain distinguishable and failure is never shown as success. |
| 2 | Needs Your Input | Progress is blocked by missing information, permission, connection or human judgement other than review or approval of a prepared artefact. |
| 3 | Ready For You | A reviewable artefact, recommendation or approval action is ready for the current viewer and that viewer is eligible to act. |
| 4 | Working | Work is queued, running, scheduled or safely retrying and no customer action is currently required. |

Provider acceptance, draft preparation or approval alone does not make an external-action item Completed.

Today is the primary current-attention surface and is broader than the Daily Briefing. It includes the timestamped Daily Briefing, due and overdue work, approvals, Needs Your Input items, and material connection or trust alerts. Today and the Daily Briefing are projections and do not own workflow state.

## PD-005 — Email-only Controlled Provider Write

The only v1 provider write is sending an email after an eligible human has reviewed and explicitly approved the exact final payload. This applies to internal and external recipients.

| Capability | Recommended v1 boundary |
|---|---|
| Read, classify and summarise authorised email | Included. |
| Prepare and edit an email response in TMOS | Included; TMOS is the system of record for the draft and approval history. |
| Create an Outlook draft | Excluded. |
| Send an email | Included only after exact-payload approval and immediate pre-send revalidation. |
| Move, delete or mark email | Excluded. |
| Read calendar | Included. |
| Suggest times or prepare meeting details | Included as TMOS content. |
| Create, modify or cancel calendar events | Excluded. |
| Prepare routine documents | Included as reviewable, downloadable or copyable TMOS artefacts. |
| Write to or share from OneDrive or SharePoint | Excluded. |
| Record a named person as an action owner | Included as internal structured information. |
| Notify or assign work to another person | Excluded. |
| Payments, contracts, permissions, security or HR decisions | Prohibited. |

Approval binds the final recipients, subject, body and attachments. A material edit invalidates approval.

Customer and system outcome vocabulary is:

1. Prepared
2. Awaiting Approval
3. Approved
4. Submitted to Microsoft
5. Sent
6. Failed
7. Delivery Status Unknown

Microsoft acceptance establishes **Submitted to Microsoft**, not Sent or Delivered. Sent requires separate sent-record evidence. TMOS does not claim Delivered without delivery evidence. An indeterminate attempt must be reconciled and must never be blindly retried.

## PD-006 — Outcome-based Activation, First Value and Probation Exit

Product telemetry records `probation_started` when Admin TeamMate enters Probation. This event is distinct from the D-001 Active lifecycle state.

**First Value** is achieved when at least one of the following occurs for live, authorised customer work:

- an authorised human accepts a reviewed output without significant rewrite;
- an associated approved controlled action completes; or
- the customer explicitly confirms that the output was useful.

Generation, login, setup and synthetic demonstration alone do not count as First Value.

All six canonical workflows may operate during Probation. Customer-specific Probation exit requires:

1. healthy mandatory integration, permission and knowledge-source checks;
2. a useful Morning Briefing;
3. successful important-email classification and a prepared response;
4. one additional applicable workflow operating successfully; and
5. demonstrated understanding of approval, Pause and connection controls.

The absence of a natural customer trigger for another workflow does not itself fail that customer’s Probation. All six workflows must nevertheless pass platform QA before release. Exit is readiness-based and is not automatic after seven days.

The beta may include a visible **Value Delivered** view containing Trusted Work Completed and a clearly labelled, conservative **Estimated time saved** measure. The calculation must be versioned and explainable. Ten hours saved per month and 70% draft acceptance are hypotheses, not release gates or customer promises.

## PD-007 — Restricted Live-data Private Beta

The private beta is limited to selected UK knowledge-based or service-led SMEs, approximately 5–50 employees, that meet all of the following conditions:

- Microsoft Entra ID work or school accounts and Exchange Online;
- one named primary licensed-user mailbox and calendar per Admin TeamMate initially;
- invited Organisation users may use TMOS, but shared provider authority is not inferred;
- explicitly selected OneDrive for Business folders and SharePoint Online sites or libraries under the approved source-ACL contract;
- English-language operation; and
- ordinary live business data only after Legal and Security beta gates pass.

The following are outside v1 beta:

- consumer Outlook accounts and Gmail;
- on-premises or hybrid Exchange;
- additional, shared, delegated, group or public-folder mailboxes;
- cross-tenant or guest Microsoft access;
- unrestricted OneDrive or SharePoint ingestion;
- intentional processing of special-category or criminal-offence data, children’s data, clinical-care data, legal casework, regulated financial decisions, HR or recruitment data, or payroll data.

Eligibility must be checked through customer attestation and technical enforcement before live connection. Until Legal and Security gates pass, only synthetic or otherwise non-live data may be used. Any exception requires an explicit Product change plus Legal, Security and Programme approval; it is not a sales exception.

# 4. Cross-discipline Impacts

| Discipline | Consequence if approved |
|---|---|
| Product | The human model, lifecycle behaviour, customer operations, attention surfaces, provider-write scope, success definitions and beta boundary become deterministic. |
| Architecture | Requires one default Workspace, bounded RBAC, prior-state lifecycle restoration, suspension fencing, deterministic Work Queue projection and external-send reconciliation. |
| UX | Requires role-aware journeys, exact approval affordances, separate Pause/Connection/Offboarding language, durable Work Queue grouping and trust-state outcomes. |
| Security | Requires action- and resource-specific authority, fail-closed approval integrity, tenant isolation, lifecycle fencing and constrained live-data eligibility. |
| Data/API | Requires exact lifecycle, role, approval, Work Queue, Microsoft outcome, ACL/lineage and telemetry contracts. |
| Testing | Requires release-blocking tenant, role, lifecycle, approval, duplicate-effect, projection and beta-eligibility suites. |
| Commercial | Supports one Admin TeamMate package while allowing several TMOS users; provider and support costs must be modelled against the restricted boundary. |

# 5. Required Review and Dependencies

Approval of this Product pack closes Product ambiguity but does not authorise implementation or live-data use.

After approval:

1. Security must approve the human authority matrix, approval integrity, suspension fencing and eligibility controls.
2. Architecture must record material choices for roles, lifecycle, projection, external-action reconciliation and the first safe implementation slice.
3. Data & Integrations must define delegated versus application access, exact Microsoft Graph scopes, consent authority, mailbox and source boundaries, sync/revocation/recovery and source-ACL preservation.
4. Legal must approve live-data prerequisites, exclusions, retention, rights and customer/provider terms.
5. UX must translate these decisions into deterministic journeys and interface states.
6. AI Behaviour must complete workflow contracts within the approved action boundary.
7. QA must define traceability and release-gate evidence.
8. Customer Success and Commercial must align activation, beta operation, packaging and claims.

# 6. Approval Record

| Field | Value |
|---|---|
| Product Manager recommendation | Proposed on 2026-08-09 |
| Accountable approval | Approved on 2026-08-09 |
| Programme reconciliation | Recorded; PD-001 through PD-007 are Active |
| Required downstream reviews | Architecture and trust-control decisions approved separately; contract evidence remains pending |
| Effective baseline | SME v1 from 2026-08-09 |

# 7. Repository Changes Required After Approval

At minimum, the following canonical documents require owner-led alignment:

- Product Requirements, Role Handbook, Workflows and Onboarding/Probation;
- Interaction Model and UX/UI Specification;
- TMOS System Architecture and required ADRs;
- Security, API, Data Model and Microsoft Integration contracts;
- Test and Evaluation Specification and requirements traceability;
- Commercial, Customer Success and Legal evidence specifications.

# 8. Execution Readiness

- Ready for Lovable: No
- Ready for Codex: No
- Decision required first: No for Product decision closure; downstream control and evidence gates still apply
- Authorised execution scope: Product decisions may be propagated into governed specifications; feature implementation requires its separate readiness gate
- Private-beta gate: Fail

# 9. Related Documents

- [Programme Baseline Audit Report](programme-baseline-audit-report.md)
- [Decision Register](decision-register.md)
- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
