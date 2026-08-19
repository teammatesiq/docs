---
Document title: TeamMates Cross-Repository Baseline Manifest
Version: 1.0
Status: Controlled
Owner: Founder and Orchestration
Baseline date: 2026-08-19
---

# 1. Purpose

This manifest identifies the exact repositories, revisions, release evidence and governance records that together define the controlled TeamMates SME v1 position.

A single repository does not contain the whole product baseline:

- `teammatesiq/docs` governs product, architecture, trust, experience, commercial and evaluation intent;
- `teammatesiq/platform` contains production application code, migrations, tests, infrastructure and release evidence;
- `teammatesiq/teammate-colleague-hub` is a non-authoritative Lovable experience reference.

# 2. Baseline components

| Component | Repository / record | Controlled reference | Role |
|---|---|---|---|
| Documentation source snapshot before reconciliation | `teammatesiq/docs` | `45849f7ca1c181ad6c3f446e46605e0a3d5949d6` | Starting point reconciled by the pull request that first contains this manifest |
| Documentation control point | `teammatesiq/docs` | The first merge commit on `main` containing version 1.0 of this manifest | Canonical cross-repository governance baseline |
| Corrected application release candidate | `teammatesiq/platform` | `48ad426950d8ce37ac8f336c89bff4d0d9b4424c` | Pinned internal-alpha application release candidate |
| Release branch | `teammatesiq/platform` | `release/sme-v1-rc1` | Immutable release-control ref for the corrected candidate |
| Platform `main` observed during reconciliation | `teammatesiq/platform` | `cdec17e4f17bfbeb7c37f96486e4baf4cdc7ac59` | Later integration head; does not automatically replace the pinned release candidate |
| Database baseline | `teammatesiq/platform` | Schema v26 | Controlled persistence version for the release candidate |
| Development deployment evidence | `teammatesiq/platform` Actions | Run `32178832787` | Successful exact release-candidate development deployment |
| Calendar permission recovery evidence | `teammatesiq/platform` Actions | Run `32243424349` | Successful exact delegated `Calendars.Read` activation and verification |
| Launch critical path | `teammatesiq/platform#106` | Current open issue | Programme delivery control |
| QA and release gate | `teammatesiq/platform#109` | Current open issue | Internal-alpha acceptance and release assurance |
| Important Email controlled acceptance | `teammatesiq/platform#88` | Current open issue | Review-only live owner acceptance; no send |
| Parallel next product slice | `teammatesiq/platform#154` | Current open issue, default-off | Trusted Draft Workbench; not part of the pinned release candidate |
| Lovable experience reference | `teammatesiq/teammate-colleague-hub` | `a2c92b8df6caca18673e5ad634a35ecdfbaedd8c` | Non-authoritative customer-experience reference |

# 3. Controlled product decisions

The baseline includes these decisions:

- Admin TeamMate is the only TeamMate in SME v1.
- Project TeamMate and all other TeamMate roles are outside SME v1.
- Initial market is UK SMEs, primarily approximately 5–50 employees using Microsoft 365.
- SME v1 uses one functional commercial package rather than multiple TeamMate packages.
- The deployed lifecycle is Configuring → Probation → Active → Suspended → Archived.
- A deployed TeamMate has no Draft state.
- Customer-facing Paused maps to `suspended/customer_paused`.
- TeamMates platform identity and connected Microsoft identity are separate boundaries.
- Connected Microsoft identity never grants TeamMates organisation membership.
- Current Microsoft access is delegated `Mail.Read` and `Calendars.Read` only.
- No Microsoft write permission, file authority or consequential external action is enabled.
- Customer-visible work remains grounded, reviewable and traceable through Today, Work Queue and Activity.

# 4. Specification interpretation

The canonical specifications include both:

- target-state requirements for the intended SME MVP; and
- the narrower current release boundary proven in the production repository.

Until a broader capability is explicitly approved, implemented, independently verified and added to a release candidate, the narrower [SME v1 Current Release Boundary](sme-v1-current-release-boundary.md) controls.

Examples of target-state capability that is not current activation authority include:

- sending email;
- writing calendar events;
- file access or sharing;
- contact access;
- autonomous external action;
- approved organisational knowledge retrieval where no current release evidence exists;
- additional TeamMate roles.

# 5. Repository authority

## 5.1 `teammatesiq/docs`

Authoritative for:

- product proposition and scope;
- TeamMate role and lifecycle;
- architecture and domain intent;
- trust, privacy and permission principles;
- UX and terminology;
- commercial strategy;
- test and evaluation policy;
- delivery operating model and cross-repository baseline.

## 5.2 `teammatesiq/platform`

Authoritative for implemented behaviour at an accepted revision, including:

- application code;
- database migrations and schema ledger;
- runtime configuration;
- Microsoft integration implementation;
- infrastructure and deployment workflows;
- automated tests and live release evidence.

Implementation may not silently redefine canonical product or trust decisions. A material difference requires reconciliation through an issue and documentation update.

## 5.3 `teammatesiq/teammate-colleague-hub`

Authoritative only as a reference for:

- visual and interaction exploration;
- customer-language exploration;
- prototype journeys and layout ideas.

It is never authoritative for permissions, policy, tenant isolation, lifecycle transitions, audit, Microsoft Graph execution, AI execution or data security.

# 6. Change-control rule

A material baseline change requires:

1. a controlling issue;
2. explicit scope, non-goals and acceptance criteria;
3. required specialist review;
4. Founder approval where a Founder gate applies;
5. a pull request with validation evidence;
6. an update to this manifest or a successor version;
7. an updated release candidate where production behaviour changes.

Merging code to `main`, changing a Lovable prototype or agreeing something only in chat does not by itself change this baseline.

# 7. Known open controls at baseline date

- Internal-alpha live signed-in acceptance remains open under #109.
- Important Email review-only owner acceptance remains open under #88.
- Monitoring, rollback, recovery and residual-risk evidence remain open under #109.
- Production launch remains a separate Founder decision.
- The Trusted Draft Workbench under #154 remains default-off and outside the pinned release candidate.
- GitHub branch protection and required-review settings must be verified independently of repository files; CODEOWNERS alone does not enforce them.

# 8. Superseded material

`teammatesiq/docs` pull request #2, formerly titled `Add TeamMates governance and integration contracts`, was closed as superseded on 19 August 2026. It must not be used as authority for Microsoft write scopes, file access, external effects or implementation beyond this baseline.