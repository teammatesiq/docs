---
Document title: TeamMates Cross-Repository Baseline Manifest
Version: 1.2
Status: Controlled
Owner: Founder and Orchestration
Baseline date: 2026-08-30
Last reconciled: 2026-08-30
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
| Documentation source snapshot before reconciliation | `teammatesiq/docs` | `45849f7ca1c181ad6c3f446e46605e0a3d5949d6` | Pre-reconciliation starting point |
| Documentation governance baseline | `teammatesiq/docs` | `239959136d124afa69f3c2ea092d91311cb2616d` / PR #5 | Established the operating model, release boundary, substantive specifications, manifest and audit |
| Documentation operating-control issue | `teammatesiq/docs#4` | Completed | Controlled the initial cross-repository reconciliation |
| Manual ChatGPT Project register | `teammatesiq/docs#6` | Open manual action | Applies the eight-authority chat structure and retires the obsolete workplace-insights direction |
| Cross-repository protected delivery paths | `teammatesiq/docs#7` | Open manual action | Coordinates branch protection/rulesets for docs, platform and Lovable repositories |
| Application release candidate | `teammatesiq/platform` | `76713a8c125f4a9b881e8d934b8b1b6d9d82f4d3` | Founder-approved schema-v26 internal-alpha candidate |
| Release branch | `teammatesiq/platform` | `release/sme-v1-rc1` | Controlled ref fast-forwarded without force and verified at the exact candidate SHA |
| Platform agent/repository governance | `teammatesiq/platform` | `76713a8c125f4a9b881e8d934b8b1b6d9d82f4d3` / PR #156 | Root/scoped agent instructions, CODEOWNERS, deterministic handoff and PR controls; Workspace run `32293629624` passed |
| Platform branch-protection control | `teammatesiq/platform#1` | Open manual action | Enforces required reviews/checks and blocks force push/deletion after GitHub settings evidence |
| Database baseline | `teammatesiq/platform` | Schema v26 | Unchanged by the approved repin |
| Exact-target full assurance | `teammatesiq/platform` Actions | Run `32293888522` | Successful complete Workspace validation at the candidate SHA |
| Superseded-candidate deployment evidence | `teammatesiq/platform` Actions | Run `32178832787` | Historical evidence for `48ad426…` only |
| Superseded-candidate calendar evidence | `teammatesiq/platform` Actions | Run `32243424349` | Historical evidence for `48ad426…` only |
| Exact-target deployment evidence | `teammatesiq/platform` Actions | Run `32629805012` | Historical evidence that `76713a8…` deployed successfully; not current-health proof |
| Current external health | `teammatesiq/platform#109` | Pending | No current externally verified healthy-state evidence |
| Renewed exact-target calendar and signed-in evidence | `teammatesiq/platform#109` | Pending | Must be repeated against the exact candidate |
| Credential-neutral development operation | `teammatesiq/platform#109` | Blocked | Must prove the cache-compatible calendar key version and preserve Entra credential key sets before deployment |
| Launch critical path | `teammatesiq/platform#106` | Open | Programme, internal-alpha and parallel-delivery control |
| Product delivery control | `teammatesiq/platform#107` | Open | Separates completed candidate scope from the controlled next-value slice |
| QA and release gate | `teammatesiq/platform#109` | Open | Internal-alpha acceptance and release assurance |
| Important Email controlled acceptance | `teammatesiq/platform#88` | Open | Review-only live owner acceptance; no send |
| Parallel next product slice | `teammatesiq/platform#154` | Open, default-off | Trusted Draft Workbench; not part of the pinned release candidate |
| Excluded later PR stack | `teammatesiq/platform` | PRs #157, #160, #162, #164 and #166 | Not included in the approved candidate |
| Lovable experience authority boundary | `teammatesiq/teammate-colleague-hub` | `4605b2ebd680d1480d75a59d8f60022c0af912ce` / PR #2 | Preserves Lovable history controls and makes experience-only authority durable |

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
- No Microsoft write permission, Graph application permission, file authority or consequential external action is enabled.
- Customer-visible work remains grounded, reviewable and traceable through Today, Work Queue and Activity.
- The Trusted Draft Workbench is an approved default-off next slice, not part of the pinned candidate.
- Founder approval under platform #106 authorises the candidate replacement only; it does not authorise deployment, activation, permission expansion, external effects, private beta or production launch.
- Production launch remains a separate Founder decision.

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

Every fresh coding-agent session is governed by the root and scoped `AGENTS.md` files merged in PR #156. Material tasks use `docs/codex-implementation-handoff.md` rather than relying on other-chat memory.

## 5.3 `teammatesiq/teammate-colleague-hub`

Authoritative only as a reference for:

- visual and interaction exploration;
- customer-language exploration;
- prototype journeys and layout ideas.

It is never authoritative for permissions, policy, tenant isolation, lifecycle transitions, audit, Microsoft Graph execution, AI execution or data security. The durable root `AGENTS.md` boundary was merged in prototype PR #2.

# 6. Authority and handoff model

The active authority model is:

1. Founder & Orchestration;
2. Product Authority;
3. Technical Design Authority;
4. Experience Authority;
5. Trust Authority;
6. AI Behaviour Authority;
7. QA & Release Assurance;
8. Commercial & Customer Success.

Data & Integrations and Platform/DevOps/Reliability support Technical Design. Legal/Privacy supports Trust. Brand supports Experience. Customer Implementation & Success supports Commercial before launch scale.

Specialists do not issue competing direct implementation prompts. Orchestration produces one controlling issue and deterministic handoff. Lovable explores experience. One primary Codex thread implements. QA independently proves the result.

The ChatGPT Project UI changes required to apply the canonical chat names remain tracked in docs issue #6.

# 7. Change-control rule

A material baseline change requires:

1. a controlling issue;
2. explicit scope, non-goals and acceptance criteria;
3. required specialist review;
4. Founder approval where a Founder gate applies;
5. a pull request with validation evidence;
6. an update to this manifest or a successor version;
7. an updated release candidate where production behaviour changes.

Merging code to `main`, changing a Lovable prototype or agreeing something only in chat does not by itself change this baseline.

# 8. Known open controls at reconciliation date

## Release and product

- Internal-alpha live signed-in acceptance remains open under platform #109.
- Important Email review-only owner acceptance remains open under platform #88.
- Development deployment remains blocked pending a credential-neutral #109 operation that preserves the exact calendar cache key and Entra credential key sets.
- Monitoring, rollback, recovery and residual-risk evidence remain open under #109.
- Production launch remains a separate Founder decision.
- The Trusted Draft Workbench under #154 remains default-off and outside the pinned release candidate.

## Manual governance

- The TeamMates ChatGPT Project chats still require UI renaming/reorganisation and obsolete-chat retirement under docs #6.
- GitHub branch protection/rulesets still require owner administration and evidence under platform #1 and docs #7.
- CODEOWNERS identifies platform ownership but has no enforcement effect until the applicable ruleset is enabled.
- Lovable connected-branch behaviour must be verified before applying a rule that could break editor synchronisation.

# 9. Superseded material

`teammatesiq/docs` pull request #2, formerly titled `Add TeamMates governance and integration contracts`, was closed as superseded on 19 August 2026. It must not be used as authority for Microsoft write scopes, file access, external effects or implementation beyond this baseline.

Any earlier TeamMates chat based on workplace analytics, collaboration scoring, meeting-load analysis, employee/person scoring or workforce-insight dashboards is outside the approved product proposition and must be retired under docs issue #6.
