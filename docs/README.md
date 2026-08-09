# TeamMates Canonical Document Register

This register indexes the canonical documentation set for the TeamMates product and TMOS platform.

The canonical specification set currently contains 18 documents: 12 substantive specifications and 6 placeholders. The register itself and baseline-control records are governance documents and are not included in that specification count.

## Classification

- **Substantive specification** — contains material approved or draft requirements, behaviour, architecture or engineering detail rather than an empty document structure.
- **Placeholder** — reserves a canonical document location but its material sections remain incomplete.
- **Governance document** — controls or records the specification set, its consistency or its baseline state.
- **Implementation artefact not yet created** — a planned executable or delivery artefact whose repository location exists but currently contains no implementation content.

## Canonical specifications

| Document name | Path | Version | Status | Classification | Purpose |
|---|---|---:|---|---|---|
| [Product Requirements](strategy/product-requirements.md) | `docs/strategy/product-requirements.md` | 1.0 | Draft | Substantive specification | Defines the TeamMates SME MVP vision, market, scope, requirements, governance and success criteria. |
| [Product Commercial Strategy](strategy/product-commercial-strategy.md) | `docs/strategy/product-commercial-strategy.md` | 1.0 | Draft | Placeholder | Provides the placeholder structure for the approved TeamMates product and commercial strategy. |
| [TMOS Platform Architecture](architecture/tmos-platform-architecture.md) | `docs/architecture/tmos-platform-architecture.md` | 1.0 | Draft | Substantive specification | Defines the logical TMOS platform architecture, component boundaries, runtime, governance and deployment philosophy. |
| [TeamMate DNA](architecture/teammate-dna.md) | `docs/architecture/teammate-dna.md` | 1.0 | Draft | Substantive specification | Defines the shared identity, behavioural, governance, memory and interaction model inherited by TeamMate roles. |
| [TeamMate Factory](architecture/teammate-factory.md) | `docs/architecture/teammate-factory.md` | 1.0 | Draft | Substantive specification | Defines how versioned TeamMate roles, capabilities and Blueprints are created, validated, released and deployed. |
| [TMOS Domain Model](architecture/tmos-domain-model.md) | `docs/architecture/tmos-domain-model.md` | 1.0 | Draft | Substantive specification | Defines TMOS domains, entities, relationships, ownership, lifecycle, tenancy and audit expectations. |
| [TeamMate Interaction Model](architecture/teammate-interaction-model.md) | `docs/architecture/teammate-interaction-model.md` | 1.0 | Draft | Substantive specification | Defines interactions between people, TeamMates and TMOS, including work, approvals, evidence and human control. |
| [TMOS System Architecture](architecture/tmos-system-architecture.md) | `docs/architecture/tmos-system-architecture.md` | 1.0 | Draft | Substantive specification | Defines the physical and software architecture for the TMOS SME MVP. |
| [Admin TeamMate Role Handbook](product/admin-teammate-role-handbook.md) | `docs/product/admin-teammate-role-handbook.md` | 1.0 | Draft | Substantive specification | Defines the Admin TeamMate role, outcomes, responsibilities, capabilities, boundaries and operating behaviour. |
| [Admin TeamMate Workflows](product/admin-teammate-workflows.md) | `docs/product/admin-teammate-workflows.md` | 1.0 | Draft | Placeholder | Provides the canonical placeholder structure for approved Admin TeamMate workflows. |
| [Admin TeamMate Onboarding and Probation](product/admin-teammate-onboarding-probation.md) | `docs/product/admin-teammate-onboarding-probation.md` | 1.0 | Draft | Placeholder | Provides the canonical placeholder structure for Admin TeamMate onboarding, validation and probation. |
| [Admin TeamMate UX/UI Specification](ux/admin-teammate-ux-ui-specification.md) | `docs/ux/admin-teammate-ux-ui-specification.md` | 1.0 | Draft | Placeholder | Provides the canonical placeholder structure for the Admin TeamMate user experience and interface specification. |
| [Security, Privacy and Governance](security/security-privacy-governance.md) | `docs/security/security-privacy-governance.md` | 1.0 | Draft | Substantive specification | Defines TeamMates and TMOS security, privacy, human-control and governance requirements. |
| [Data Model and Database Schema](engineering/data-model-database-schema.md) | `docs/engineering/data-model-database-schema.md` | 1.0 | Draft | Substantive specification | Defines the PostgreSQL relational data model, tenancy controls, persistence and audit structures for the SME MVP. |
| [API Contract and Service Interfaces](engineering/api-contract-service-interfaces.md) | `docs/engineering/api-contract-service-interfaces.md` | 1.0 | Draft | Substantive specification | Defines the TMOS API resources, service boundaries, events and integration contracts for the SME MVP. |
| [Engineering Release Plan](engineering/engineering-release-plan.md) | `docs/engineering/engineering-release-plan.md` | 1.0 | Draft | Placeholder | Provides the canonical placeholder structure for sequencing and governing TeamMates engineering releases. |
| [Test and Evaluation Specification](engineering/test-evaluation-specification.md) | `docs/engineering/test-evaluation-specification.md` | 1.0 | Draft | Placeholder | Provides the canonical placeholder structure for testing and evaluating TeamMates and TMOS. |
| [Microsoft 365 Integration Contract](engineering/microsoft-integration-contract.md) | `docs/engineering/microsoft-integration-contract.md` | 1.0 | Proposed | Substantive specification | Defines the delegated Microsoft identity, Graph scope, controlled email, reconciliation, selected-source and disconnect contract for SME v1. |

## Governance documents and baseline controls

| Item | Repository path | Classification | Current state |
|---|---|---|---|
| Canonical Document Register | `docs/README.md` | Governance document | Current register. |
| [Programme Baseline Audit Brief](governance/programme-baseline-audit-brief.md) | `docs/governance/programme-baseline-audit-brief.md` | Governance document | Current audit instruction and preliminary control assessment. |
| [Programme Baseline Audit Report](governance/programme-baseline-audit-report.md) | `docs/governance/programme-baseline-audit-report.md` | Governance document | Reconciles all 11 specialist reviews against commit `9846ba9`; current verdict is not ready for execution. |
| [Decision Register](governance/decision-register.md) | `docs/governance/decision-register.md` | Governance document | Records P-001 and D-001 as Active and identifies unresolved decision references. |
| [SME v1 Product Decision Pack](governance/product-decision-pack.md) | `docs/governance/product-decision-pack.md` | Approved governance document | Records PD-001 through PD-007 as approved and Active on 2026-08-09; downstream execution gates remain open. |
| [SME v1 Architecture and Trust-Control Decision Pack](governance/architecture-trust-control-decision-pack.md) | `docs/governance/architecture-trust-control-decision-pack.md` | Approved governance document | Records ATC-001 through ATC-008 as approved and Active on 2026-08-09; ADR, integration-contract and evidence gates remain open. |
| [TMOS Authority and Model-context Precedence Proposal](governance/ai-authority-decision-proposal.md) | `docs/governance/ai-authority-decision-proposal.md` | Proposed governance document | Proposes AI-001 after Security, Architecture and QA review; it remains non-binding until explicitly approved and recorded. |
| Baseline manifest | Not yet created | Governance document | No baseline manifest exists in the repository. |

## Implementation artefact status

| Artefact | Repository location | Classification | Current state |
|---|---|---|---|
| Engineering backlog | `engineering/backlog/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Architecture decision records | `engineering/adr/` | Proposed implementation contracts | ADR-011 through ADR-017 implement ATC-001 through ATC-008 and await specialist acceptance evidence. |
| C4 diagrams | `architecture/c4/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Sequence diagrams | `architecture/sequence/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Entity-relationship diagrams | `architecture/erd/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| OpenAPI specification | `api/openapi/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Database migrations | `database/migrations/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |

## Proposed architecture decision records

| ADR | Implements | Status |
|---|---|---|
| [ADR-011 Tenant Context, RLS and Trusted Worker Envelope](../engineering/adr/ADR-011-tenant-context-rls-trusted-worker-envelope.md) | ATC-001, ATC-008 | Proposed |
| [ADR-012 Lifecycle Transition Service and Suspension Fence](../engineering/adr/ADR-012-lifecycle-transition-suspension-fence.md) | ATC-002, ATC-003 | Proposed |
| [ADR-013 Controlled-action Approval Integrity](../engineering/adr/ADR-013-controlled-action-approval-integrity.md) | ATC-004 | Proposed |
| [ADR-014 Microsoft Email Send and Reconciliation](../engineering/adr/ADR-014-microsoft-email-send-reconciliation.md) | ATC-005 | Proposed |
| [ADR-015 Delegated Microsoft Access and Consent](../engineering/adr/ADR-015-delegated-microsoft-access-consent.md) | ATC-006 | Proposed |
| [ADR-016 Selected Knowledge Access and ACL Lineage](../engineering/adr/ADR-016-selected-knowledge-access-acl-lineage.md) | ATC-007 | Proposed |
| [ADR-017 Transactional Outbox, Idempotency and Audit Reconstruction](../engineering/adr/ADR-017-transactional-outbox-idempotency-audit.md) | ATC-008 | Proposed |

Classification records repository completeness; it does not approve a document or make the repository ready to baseline. The 17 pre-existing canonical specifications remain Draft; the Microsoft 365 Integration Contract is Proposed.
