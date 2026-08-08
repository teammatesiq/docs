# TeamMates Canonical Document Register

This register indexes the canonical documentation set for the TeamMates product and TMOS platform.

The canonical specification set currently contains 17 documents: 11 substantive specifications and 6 placeholders. The register itself and baseline-control records are governance documents and are not included in that specification count.

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

## Governance documents and baseline controls

| Item | Repository path | Classification | Current state |
|---|---|---|---|
| Canonical Document Register | `docs/README.md` | Governance document | Current register. |
| Cross-document consistency audit | Not yet created | Governance document | No current audit record exists in the repository. |
| Baseline manifest | Not yet created | Governance document | No baseline manifest exists in the repository. |

## Implementation artefact status

| Artefact | Repository location | Classification | Current state |
|---|---|---|---|
| Engineering backlog | `engineering/backlog/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Architecture decision records | `engineering/adr/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| C4 diagrams | `architecture/c4/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Sequence diagrams | `architecture/sequence/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Entity-relationship diagrams | `architecture/erd/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| OpenAPI specification | `api/openapi/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |
| Database migrations | `database/migrations/` | Implementation artefact not yet created | Directory contains only `.gitkeep`. |

Classification records repository completeness; it does not approve a document or make the repository ready to baseline. All 17 canonical specifications remain Draft.
