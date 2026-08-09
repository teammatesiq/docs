---
Document title: Sprint 1 Engineering Backlog
Version: 1.0
Status: Approved
Owner: TeamMates Engineering
Last updated: 2026-08-09
---

# 1. Sprint outcome

Build and deploy the production-shaped TeamMates application skeleton so an authenticated development user can reach the empty TeamMates shell and an engineer can trace the request through the web, API and structured logs.

Sprint length is two weeks. Planned capacity is two full-time engineers, with part-time Product, UX and security/cloud support. The sprint is limited to foundation work; it does not implement customer onboarding, TeamMate deployment, Microsoft data access, AI work or production release.

# 2. Sprint commitment

| ID | Story | Owner profile | Estimate | Dependency |
|---|---|---|---:|---|
| S1-001 | Establish the application repository and contribution controls | Full-stack | 3 points | None |
| S1-002 | Scaffold the TypeScript application workspace | Full-stack | 5 points | S1-001 |
| S1-003 | Enforce local and CI quality gates | Full-stack | 3 points | S1-002 |
| S1-004 | Implement typed configuration and secret boundaries | Backend/AI | 3 points | S1-002 |
| S1-005 | Deliver API health, readiness and error foundations | Backend/AI | 5 points | S1-004 |
| S1-006 | Deliver the responsive web and authenticated shell | Full-stack | 5 points | S1-002, S1-004 |
| S1-007 | Deliver the worker runtime skeleton | Backend/AI | 3 points | S1-002, S1-004 |
| S1-008 | Add request correlation and structured observability | Backend/AI | 3 points | S1-005, S1-007 |
| S1-009 | Automate development deployment, smoke test and rollback | Full-stack | 5 points | S1-003, S1-005–S1-008 |
| S1-010 | Record the minimum provider implementation decisions | Shared | 2 points | Can run in parallel |

Total committed estimate: **37 points**. Story points are relative planning units, not hours. S1-001 and provider provisioning start on day one; S1-002 through S1-008 may use local substitutes while external access is being provisioned.

# 3. Build-ready stories

## S1-001 — Establish the application repository and contribution controls

**User story:** As an engineer, I need a dedicated TeamMates application repository so deployable code is versioned independently from canonical specifications.

**Acceptance criteria:**

1. Repository is named `teammatesiq/platform`, is private, and has `main` as its default branch.
2. Repository contains a concise README linking to the canonical `teammatesiq/docs` baseline and identifying Admin TeamMate as SME v1 scope.
3. Pull requests require green build, lint, type-check, test, secret-scan and dependency-scan checks before merge.
4. Force pushes and branch deletion are disabled for `main`.
5. Required review and CODEOWNERS rules identify Engineering ownership; security-sensitive paths require the nominated security reviewer once that person is named.
6. No application source is committed to `teammatesiq/docs`.

**Evidence:** Repository settings capture; first protected pull request; passing required checks.

## S1-002 — Scaffold the TypeScript application workspace

**User story:** As an engineer, I need one modular workspace for the web, API, worker and shared packages so the modular-monolith boundary is visible from the first commit.

**Acceptance criteria:**

1. Workspace uses a pinned Node.js version and a lockfile-backed package manager.
2. It contains `apps/web`, `apps/api`, `apps/worker` and shared packages for configuration, contracts, domain and observability.
3. Each application starts locally through documented commands.
4. Package boundaries prevent UI code from importing backend implementation modules.
5. A clean checkout can install and build without undeclared local dependencies.

**Tests:** Workspace build smoke test; package-boundary test; clean-install CI job.

## S1-003 — Enforce local and CI quality gates

**User story:** As a delivery team, we need automated quality checks on every change so defects and unsafe dependencies are blocked before merge.

**Acceptance criteria:**

1. Formatting, linting, strict TypeScript checking and unit tests run from root commands.
2. CI runs the same commands on every pull request and on `main`.
3. CI includes secret scanning and production-dependency vulnerability scanning.
4. Test reports and build artefacts are retained for failed runs.
5. A deliberately failing fixture proves each required check blocks merge, then is removed.

**Tests:** CI workflow validation; known-failure demonstration; clean main run.

## S1-004 — Implement typed configuration and secret boundaries

**User story:** As an operator, I need configuration to fail safely and secrets to remain outside source control so deployments are reproducible without credential leakage.

**Acceptance criteria:**

1. Each runtime validates required environment variables at startup using a typed schema.
2. Public browser configuration is explicitly separated from server-only configuration.
3. Development, test and deployed environments have documented configuration contracts without real secret values.
4. Missing or invalid mandatory configuration prevents readiness and produces a safe diagnostic.
5. Repository secret scanning covers history introduced during the sprint.

**Tests:** Valid, missing, malformed and accidental-public-secret configuration cases.

## S1-005 — Deliver API health, readiness and error foundations

**User story:** As an operator, I need distinct liveness and readiness signals plus consistent safe errors so platform health can be automated and diagnosed.

**Acceptance criteria:**

1. `GET /health/live` confirms only that the API process is running.
2. `GET /health/ready` checks configured critical dependencies and returns non-ready when any mandatory dependency is unavailable.
3. API responses include a correlation identifier and use one versioned error envelope.
4. Errors do not expose stack traces, credentials, tokens or internal infrastructure details.
5. Shutdown stops new traffic and allows bounded in-flight completion.

**Tests:** Liveness, readiness success/failure, error-redaction and graceful-shutdown integration tests.

## S1-006 — Deliver the responsive web and authenticated shell

**User story:** As a development user, I need to sign in and reach the TeamMates shell so the first end-to-end delivery path is demonstrable.

**Acceptance criteria:**

1. The web application provides loading, signed-out, authentication-failure and authenticated-shell states.
2. Authentication is behind a feature flag and uses the configured development identity route; no hard-coded identity bypass is available in deployed environments.
3. The shell uses approved TeamMatesIQ and TeamMates terminology and does not expose Project TeamMate or deferred capabilities.
4. Keyboard navigation, visible focus, landmark structure and responsive behaviour pass the Sprint 1 accessibility smoke check.
5. A signed-out user cannot access the authenticated route.

**Tests:** Component states; route protection; feature-flag cases; Playwright desktop/mobile smoke journey.

## S1-007 — Deliver the worker runtime skeleton

**User story:** As an engineer, I need a separately runnable background worker so asynchronous work has a production-shaped execution boundary before Microsoft or AI jobs are added.

**Acceptance criteria:**

1. Worker starts independently using the shared configuration and observability packages.
2. It exposes process health through the chosen platform mechanism without opening an unauthenticated business endpoint.
3. It handles termination gracefully and stops accepting new work before exit.
4. A no-op development job proves enqueue, consume and acknowledgement wiring without containing customer data.
5. Retry configuration is explicit and bounded.

**Tests:** Startup, no-op consumption, graceful shutdown and bounded-retry tests.

## S1-008 — Add request correlation and structured observability

**User story:** As an engineer, I need one traceable request path so failures can be diagnosed across web, API and worker without logging sensitive content.

**Acceptance criteria:**

1. API accepts or creates a validated correlation ID and returns it to the caller.
2. Structured logs include timestamp, service, environment, severity and correlation ID.
3. The no-op job carries causation and correlation identifiers from enqueue to worker completion.
4. Logging rules prohibit tokens, credentials, mailbox/document content and raw personal data.
5. The sprint demo request is reconstructable from deployed logs.

**Tests:** Correlation propagation; invalid-ID replacement; sensitive-field redaction; log-schema test.

## S1-009 — Automate development deployment, smoke test and rollback

**User story:** As a delivery team, we need every accepted `main` change deployed predictably to development so working software is continuously demonstrable.

**Acceptance criteria:**

1. Merge to `main` produces immutable versioned artefacts and deploys web, API and worker to development.
2. Deployment waits for readiness and runs the authenticated-shell and health smoke tests.
3. A failed readiness or smoke check stops or reverses the rollout automatically.
4. The documented rollback procedure restores the previous known-good artefact without rebuilding it.
5. One rollback rehearsal is completed and evidenced during the sprint.

**Tests/evidence:** Successful deployment run; failed-rollout test; smoke-test output; rollback record.

## S1-010 — Record the minimum provider implementation decisions

**User story:** As the engineering team, we need the unresolved provider choices that affect Sprint 1 recorded so scaffolding and deployment use supported, reviewable technology.

**Acceptance criteria:**

1. ADRs identify the selected hosting/runtime, PostgreSQL, queue, object storage, secrets, identity and observability providers where the baseline leaves a choice open.
2. Each ADR records decision drivers, rejected options, security/data impact, cost assumptions and reversibility.
3. Decisions preserve the approved modular-monolith, tenant, Microsoft-first and deployment boundaries.
4. ADRs do not redefine product scope or approve beta/production release.

**Evidence:** Accepted ADRs linked from the application README and Sprint 1 review record.

# 4. Day-one enabling actions

These are mobilisation actions rather than engineering stories and must be owned on day one:

| Action | Accountable owner | Needed by |
|---|---|---|
| Name the two engineers and their availability | Product Owner | Sprint planning |
| Name UX and security/cloud support | Product Owner | Sprint planning |
| Create `teammatesiq/platform` with required admin permissions | Repository owner | Day 1 |
| Provision development Microsoft Entra tenant/app and test accounts | Engineering | Day 3 |
| Provision selected development cloud services and secret store | Engineering/Cloud | Day 4 |
| Create OpenAI project with budget and data controls | Engineering/Product | Day 4 |
| Confirm development domain and DNS owner | Product/Cloud | Day 4 |

# 5. Sprint-level acceptance

Sprint 1 is accepted only when:

1. all committed stories meet their acceptance criteria or are explicitly removed and reforecast by the Product Owner;
2. a development user completes the signed-out-to-authenticated-shell journey;
3. the deployed web request is traceable through API logs with a correlation ID;
4. web, API and worker report healthy through the deployment platform;
5. CI, smoke and rollback evidence is attached to the sprint review;
6. no secret is committed and no Critical or High dependency/security finding remains untreated; and
7. the next sprint can begin identity and tenant-isolation work without restructuring the repository.

# 6. Traceability

- [Approved MVP Sprint Plan](admin-teammate-mvp-sprint-plan.md)
- [Engineering Release Plan and MVP Backlog](../../docs/engineering/engineering-release-plan.md)
- [Platform Architecture](../../docs/architecture/tmos-platform-architecture.md)
- [Security, Privacy and Governance](../../docs/security/security-privacy-governance.md)
- [Test and Evaluation Specification](../../docs/engineering/test-evaluation-specification.md)
- Baseline scope: E0.1 and part of E0.2; NFR-003 and NFR-009
