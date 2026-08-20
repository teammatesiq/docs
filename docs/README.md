# TeamMates Canonical Document Register

This register indexes the canonical documentation set for the TeamMates product and TMOS platform.

As of 19 August 2026, the canonical specification set contains **17 substantive specifications and no placeholders**. Specifications have different approval states; classification describes completeness, not release authority.

The exact current release boundary is governed by:

- [SME v1 Current Release Boundary](governance/sme-v1-current-release-boundary.md);
- [Cross-Repository Baseline Manifest](governance/cross-repository-baseline-manifest.md);
- [Delivery Operating Model](governance/delivery-operating-model.md).

Broader future-looking wording in a Draft specification does not authorise additional implementation, provider permission, external effect or production launch.

## 1. Source-of-truth topology

| Repository / record | Authority |
|---|---|
| `teammatesiq/docs` | Product, architecture, trust, experience, commercial, evaluation and operating-model intent |
| `teammatesiq/platform` | Accepted implementation, migrations, tests, infrastructure and release evidence at an exact revision |
| `teammatesiq/teammate-colleague-hub` | Non-authoritative Lovable customer-experience reference |
| GitHub issues and accepted Founder decisions | Current delivery control, scope decisions and release gates |
| Chat history | Working context only; not the sole durable authority |

When sources conflict, use the Delivery Operating Model and route the conflict to Orchestration rather than silently choosing or combining positions.

## 2. Classification

- **Substantive specification** — contains material requirements, behaviour, architecture, commercial or evaluation detail rather than an empty document structure.
- **Governance document** — controls or records authority, consistency, brand, baseline or delivery state.
- **Implementation artefact** — executable code, migration, schema, workflow, infrastructure or delivery backlog.
- **Controlled** — approved for the stated purpose and scope.
- **Draft** — substantive but still contains target-state or unresolved content; it does not override the controlled current release boundary.

## 3. Canonical specifications

| Document name | Path | Version | Status | Classification | Purpose |
|---|---|---:|---|---|---|
| [Product Requirements](strategy/product-requirements.md) | `docs/strategy/product-requirements.md` | 1.0 | Draft | Substantive specification | Defines the TeamMates SME MVP vision, market, target capability, governance and success criteria. Current implementation is narrower where the release-boundary record says so. |
| [Product Commercial Strategy](strategy/product-commercial-strategy.md) | `docs/strategy/product-commercial-strategy.md` | 1.1 | Controlled | Substantive specification | Defines the UK SME wedge, one-package approach, founder-led route to market, beta qualification and commercial evidence model. |
| [TMOS Platform Architecture](architecture/tmos-platform-architecture.md) | `docs/architecture/tmos-platform-architecture.md` | 1.0 | Draft | Substantive specification | Defines logical TMOS architecture, component boundaries, runtime, governance and deployment philosophy. |
| [TeamMate DNA](architecture/teammate-dna.md) | `docs/architecture/teammate-dna.md` | 1.0 | Draft | Substantive specification | Defines shared identity, behavioural, governance, memory and interaction principles inherited by TeamMate roles. |
| [TeamMate Factory](architecture/teammate-factory.md) | `docs/architecture/teammate-factory.md` | 1.0 | Draft | Substantive specification | Defines how versioned TeamMate roles, capabilities and Blueprints are created, evaluated and released. |
| [TMOS Domain Model](architecture/tmos-domain-model.md) | `docs/architecture/tmos-domain-model.md` | 1.0 | Draft | Substantive specification | Defines TMOS domains, entities, ownership, lifecycle, tenancy and audit expectations. |
| [TeamMate Interaction Model](architecture/teammate-interaction-model.md) | `docs/architecture/teammate-interaction-model.md` | 1.0 | Draft | Substantive specification | Defines interactions between people, TeamMates and TMOS, including work, evidence and human control. |
| [TMOS System Architecture](architecture/tmos-system-architecture.md) | `docs/architecture/tmos-system-architecture.md` | 1.0 | Draft | Substantive specification | Defines physical and software architecture for the TMOS SME MVP. |
| [Admin TeamMate Role Handbook](product/admin-teammate-role-handbook.md) | `docs/product/admin-teammate-role-handbook.md` | 1.0 | Draft | Substantive specification | Defines the Admin TeamMate role, target responsibilities, boundaries and operating behaviour. Current activation remains subject to the release boundary. |
| [Admin TeamMate Workflows](product/admin-teammate-workflows.md) | `docs/product/admin-teammate-workflows.md` | 1.1 | Controlled | Substantive specification | Defines common workflow invariants, the current workflow catalogue and the default-off Trusted Draft Workbench boundary. |
| [Admin TeamMate Onboarding and Probation](product/admin-teammate-onboarding-probation.md) | `docs/product/admin-teammate-onboarding-probation.md` | 1.1 | Controlled | Substantive specification | Defines identity, connection, lifecycle, onboarding, probation, first-value and pause/recovery behaviour. |
| [Admin TeamMate UX/UI Specification](ux/admin-teammate-ux-ui-specification.md) | `docs/ux/admin-teammate-ux-ui-specification.md` | 1.1 | Controlled | Substantive specification | Defines Today, Work Queue, Activity, onboarding, evidence, content, accessibility and Lovable reference boundaries. |
| [Security, Privacy and Governance](security/security-privacy-governance.md) | `docs/security/security-privacy-governance.md` | 1.0 | Draft | Substantive specification | Defines security, privacy, tenant, permission, human-control and governance requirements. |
| [Data Model and Database Schema](engineering/data-model-database-schema.md) | `docs/engineering/data-model-database-schema.md` | 1.0 | Draft | Substantive specification | Defines target PostgreSQL data structures, tenancy controls, persistence and audit expectations. Executed migrations live in `teammatesiq/platform`. |
| [API Contract and Service Interfaces](engineering/api-contract-service-interfaces.md) | `docs/engineering/api-contract-service-interfaces.md` | 1.0 | Draft | Substantive specification | Defines target API resources, services and events. Accepted production code/contracts at the pinned release revision govern implemented behaviour. |
| [Engineering Release Plan](engineering/engineering-release-plan.md) | `docs/engineering/engineering-release-plan.md` | 1.1 | Controlled | Substantive specification | Defines the exact release candidate, streams, milestones, quality gates, deployment, rollback and Founder launch gate. |
| [Test and Evaluation Specification](engineering/test-evaluation-specification.md) | `docs/engineering/test-evaluation-specification.md` | 1.1 | Controlled | Substantive specification | Defines automated, signed-in, live, AI-behaviour, security, reliability, accessibility and release evidence. |

## 4. Baseline and operating governance

| Document | Path | Version | Status | Purpose |
|---|---|---:|---|---|
| [Delivery Operating Model](governance/delivery-operating-model.md) | `docs/governance/delivery-operating-model.md` | 1.0 | Controlled | Defines authority, chat roles, handoffs, Founder gates and the mandatory delivery route. |
| [SME v1 Current Release Boundary](governance/sme-v1-current-release-boundary.md) | `docs/governance/sme-v1-current-release-boundary.md` | 1.0 | Controlled | Defines exact product, permission, workflow and no-external-effect scope for the pinned candidate. |
| [Cross-Repository Baseline Manifest](governance/cross-repository-baseline-manifest.md) | `docs/governance/cross-repository-baseline-manifest.md` | 1.1 | Controlled | Identifies exact repository revisions, governance-control commits, schema, deployment evidence and cross-repository authority. |
| [Consistency Audit — 19 August 2026](governance/consistency-audit-2026-08-19.md) | `docs/governance/consistency-audit-2026-08-19.md` | 1.0 | Controlled audit record | Records drift findings, remediation and remaining manual controls. |
| Canonical Document Register | `docs/README.md` | Current | Controlled | Indexes and classifies the canonical set. |

## 5. Brand governance documents

| Document name | Path | Version | Status | Purpose |
|---|---|---:|---|---|
| [Brand Foundation](brand/brand-foundation.md) | `docs/brand/brand-foundation.md` | 0.1 | Current | Approved brand architecture, audience, positioning, promise, personality and creative direction. |
| [Messaging Architecture](brand/messaging-architecture.md) | `docs/brand/messaging-architecture.md` | 0.1 | Current | Customer-facing message hierarchy and touchpoint priorities. |
| [Tone, Terminology and Naming](brand/tone-terminology-and-naming.md) | `docs/brand/tone-terminology-and-naming.md` | 0.1 | Current | Naming, lifecycle language, terminology, tone and editorial usage. |
| [Claims Register](brand/claims-register.md) | `docs/brand/claims-register.md` | 0.1 | Current | Proposition, capability, evidence-backed, beta and prohibited claims. |
| [Visual Identity](brand/visual-identity.md) | `docs/brand/visual-identity.md` | 1.0 | Current | The Flow, colour, typography, imagery, brand-lockup and canonical Flow Path v1 assets. |
| [Brand Decision Log](brand/brand-decision-log.md) | `docs/brand/brand-decision-log.md` | 1.0 | Current | Approved brand decisions and implementation actions. |

## 6. Implementation and delivery artefacts

Executable implementation is intentionally held in `teammatesiq/platform`, not duplicated into this documentation repository.

| Artefact | Location | Current state |
|---|---|---|
| Approved MVP sprint plan | `engineering/backlog/admin-teammate-mvp-sprint-plan.md` | Present in this repository |
| Approved Sprint 1 backlog | `engineering/backlog/sprint-01-engineering-backlog.md` | Present in this repository |
| Application code | `teammatesiq/platform/apps` and `packages` | Production-shaped implementation present |
| Database migrations | `teammatesiq/platform` migration paths | Implemented through schema v26 for the pinned release candidate |
| Runtime/deployment infrastructure | `teammatesiq/platform/infra`, scripts and workflows | Implemented and used for verified development deployment |
| Automated assurance | `teammatesiq/platform` tests and GitHub Actions | Extensive build, boundary, config, persistence, security and browser evidence present |
| Architecture decision records in this repository | `engineering/adr/` | Legacy planned folder remains incomplete; implementation decisions are currently traceable through issues/PRs and should be consolidated when materially useful |
| C4, sequence and ERD exports in this repository | `architecture/` | Legacy planned folders remain incomplete; code, runtime docs and migrations currently contain the implemented detail |
| Standalone OpenAPI export in this repository | `api/openapi/` | Not currently maintained as an executable artefact; accepted code/contracts govern implemented routes |

An empty legacy artefact folder is not, by itself, a release blocker when the required behaviour and evidence exist elsewhere in the controlled baseline. Material undocumented implementation behaviour remains a reconciliation defect.

## 7. Current release summary

The controlled internal-alpha candidate is:

- Admin TeamMate only;
- application SHA `48ad426950d8ce37ac8f336c89bff4d0d9b4424c`;
- schema v26;
- delegated `Mail.Read` and `Calendars.Read` only;
- no Microsoft write permission, file authority or consequential external effect;
- release gate under `teammatesiq/platform#109`;
- Trusted Draft Workbench under #154 default-off and outside the candidate.

## 8. Change-control expectations

A substantive documentation change should:

- identify the controlling issue/decision;
- state whether it changes current release scope or only target-state intent;
- preserve exact lifecycle and permission language;
- update this register when a canonical document changes version/status;
- update the baseline manifest when a controlled repository revision or release boundary changes;
- use a pull request;
- avoid secrets, credentials or customer content.

## 9. Superseded material

Docs pull request #2 was closed without merge as superseded on 19 August 2026. It is not authority for Microsoft write permissions, file access, external effects or implementation outside the controlled baseline.