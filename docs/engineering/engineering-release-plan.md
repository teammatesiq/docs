---
Document title: TeamMates Engineering Release Plan
Version: 1.1
Status: Controlled
Owner: Technical Design and QA-Release Authorities
Last updated: 2026-08-19
---

# 1. Purpose

This document defines how TeamMates SME v1 changes are sequenced, integrated, assured, deployed and promoted.

The immediate objective is to reach a commercially testable Admin TeamMate through the shortest safe path while preserving tenant isolation, read-only Microsoft permissions, truthful human control and reversible deployment.

# 2. Release principles

1. Deliver complete customer outcomes, not isolated infrastructure.
2. Reuse the production-shaped modular monolith and existing workflow patterns.
3. Keep the current release candidate immutable while acceptance is in progress.
4. Separate merge, deployment, feature activation and production launch.
5. Fail closed for identity, tenancy, permission, lifecycle and stale-version uncertainty.
6. Keep Microsoft access at the minimum approved delegated scope.
7. Batch live evidence at a completed-slice or release-candidate boundary.
8. Do not allow next-slice work to displace the launch gate.
9. Record exact revisions, schema, workflow runs and residual risks.
10. Require explicit Founder approval for production launch or material boundary expansion.

# 3. Controlled release baseline

| Item | Controlled value |
|---|---|
| Product | Admin TeamMate, SME v1 |
| Application repository | `teammatesiq/platform` |
| Corrected release-candidate SHA | `48ad426950d8ce37ac8f336c89bff4d0d9b4424c` |
| Pinned release branch | `release/sme-v1-rc1` |
| Database schema | v26 |
| Development deployment run | `32178832787` — successful |
| Calendar recovery run | `32243424349` — successful |
| Microsoft permissions | Delegated `Mail.Read` and `Calendars.Read` only |
| External effects | None enabled |
| Launch control | `teammatesiq/platform#106` |
| QA/release gate | `teammatesiq/platform#109` |
| Important Email live acceptance | `teammatesiq/platform#88` |
| Parallel next slice | `teammatesiq/platform#154`, default-off and outside candidate |

The current platform `main` branch may contain later fixes or next-slice work. It does not replace the controlled release candidate without an explicit repin and renewed evidence.

# 4. Release scope

## 4.1 Customer paths under acceptance

- Morning Briefing;
- Important Email;
- Meeting Preparation;
- Meeting Follow-Up;
- Overdue Action;
- Document Request;
- cross-slice Today, Work Queue and Activity consistency.

## 4.2 Current effect boundary

The release may read authorised email and calendar data and prepare internal/review-only work.

It may not:

- send, reply to or forward email;
- mutate a mailbox;
- create, update or delete calendar events;
- contact recipients or attendees;
- read or write files;
- use Graph application permissions;
- execute another consequential external action.

# 5. Delivery streams

## 5.1 Programme and launch control — #106

Owns:

- the P0 launch path;
- sequencing and scope control;
- preventing non-critical platform work entering the launch path;
- Founder gates and release decision points.

## 5.2 Product vertical slices — #107 and linked issues

Owns complete customer outcomes from source/trigger through Work Queue, human control and Activity.

Product implementation reopens only for:

- an approved next slice;
- a proven P0 customer, safety or correctness defect;
- an explicit Founder scope decision.

## 5.3 QA and release assurance — #109

Owns:

- exact release-candidate assurance;
- development deployment evidence;
- live signed-in acceptance;
- monitoring, rollback and recovery evidence;
- residual-risk record;
- production recommendation.

## 5.4 Parallel next slice — #154

The Trusted Draft Workbench may progress in parallel only when:

- its feature remains default-off;
- it reuses existing architecture and Work Queue patterns;
- no Microsoft write permission or external effect is introduced;
- it cannot replace the pinned release candidate before #109 closes;
- it receives its own independent assurance.

# 6. Completed delivery milestones

## M1 — Production-shaped workspace

Completed foundations include:

- separately runnable Next.js web, Node.js API and worker;
- shared configuration, contracts, domain and observability packages;
- container packaging and Azure Container Apps deployment;
- provider-neutral queue boundary and Azure Service Bus adapter;
- passwordless Azure/PostgreSQL identity and persistence boundaries;
- deterministic checksummed database migrations;
- tenant-aware organisation membership;
- separate TeamMates sign-in and delegated Microsoft connector identities;
- content-safe correlation, causation and operational logs.

## M2 — Admin TeamMate customer slices

Completed customer slices through schema v26 include:

- Important Email foundations and controlled review-only drafting;
- Meeting Preparation;
- Meeting Follow-Up;
- Overdue Action;
- Document Request;
- cross-slice Today and Work Queue polish.

## M3 — Corrected release candidate

Completed:

- Microsoft partial delta-response correction;
- CI affected-area and timeout correction;
- exact release-candidate pinning;
- owner-controlled release orchestration;
- development OIDC and bounded calendar-secret recovery;
- exact delegated `Calendars.Read` verification.

# 7. Remaining milestones

## M4 — Internal-alpha live acceptance

Required under #109:

- one signed-in live development acceptance for Morning Briefing;
- one signed-in live development acceptance for each of the five customer workflows;
- Important Email review-only owner acceptance under #88;
- consistent Today, Work Queue and Activity evidence;
- verification that nothing is sent or mutated externally.

## M5 — Operational readiness

Required:

- monitoring evidence for critical services and customer paths;
- rollback evidence bound to immutable image digests and schema rules;
- recovery evidence for the required permission and secret boundaries;
- incident and support route;
- residual-risk register;
- production release recommendation.

## M6 — Founder production decision

Founder reviews:

- completed non-Founder gates;
- customer-path evidence;
- security, privacy and legal recommendation;
- operational readiness;
- costs and residual risks;
- beta/customer-support readiness.

Production is not authorised until the Founder decision is recorded.

## M7 — Controlled production deployment

After approval:

- deploy the exact approved revision and immutable images;
- apply only the approved migrations;
- preserve provider and permission boundaries;
- verify readiness, identity, persistence and connectors;
- perform bounded smoke/live acceptance;
- retain deployment and rollback evidence;
- begin with a controlled cohort rather than broad activation.

# 8. Change classes

## 8.1 P0 release defect

Examples:

- tenant-isolation failure;
- credential exposure;
- data corruption or loss;
- incorrect external effect;
- migration failure;
- broken signed-in customer path;
- release-critical outage;
- unverified required runtime permission.

P0 defects may enter the release path immediately with QA control.

## 8.2 P1 product or operational improvement

May proceed only when it does not displace P0 release evidence or broaden the controlled candidate without approval.

## 8.3 P2 refinement

Formatting, dormant-capability hardening and speculative platform abstractions remain outside the launch path unless they address a proven blocker.

# 9. Branch and pull-request controls

Every substantive change must:

- originate from a linked issue;
- use a bounded feature/fix branch;
- state customer or operational outcome;
- state scope and non-goals;
- identify canonical references;
- declare permission, external-effect, tenant, lifecycle and cost impact;
- include tests and evidence;
- update documentation where behaviour changes;
- use pull-request review before merge.

Repository settings should enforce:

- protected `main`;
- required status checks;
- blocked force push and branch deletion;
- required review;
- CODEOWNERS for sensitive paths;
- secret and dependency scanning.

At the baseline date, GitHub reported `main` as unprotected. Issue #1 remains the control item for enforcing and evidencing these settings.

# 10. Implementation sequencing

For each customer slice:

1. define the signed-in customer outcome;
2. identify an authorised source/trigger;
3. define grounding and missing-information behaviour;
4. reuse the existing durable work and Work Queue pattern;
5. add only required persistence fields and at most one append-only migration unless a P0 fix requires otherwise;
6. deliver server enforcement and UI together;
7. add Activity/terminal evidence;
8. prove tenant, lifecycle, stale and replay behaviour;
9. run affected tests;
10. merge only when the complete slice is reviewable;
11. batch live evidence at the slice/release boundary.

Do not create a scheduler, generic workflow engine, lease engine, connector platform or new horizontal service solely for hypothetical future work.

# 11. Quality gates

## 11.1 Pull-request gate

Applicable checks must cover:

- exact Node/npm toolchain;
- build;
- lint and strict TypeScript;
- unit/component tests;
- configuration and secret boundaries;
- architecture/import boundaries;
- persistence and migration behaviour;
- security-sensitive invariants;
- browser acceptance for affected signed-in journeys;
- dependency and secret scanning where configured.

## 11.2 Main integration gate

Full integration assurance runs against the merged revision and verifies that affected-area optimisations did not hide cross-slice failure.

## 11.3 Release-candidate gate

- exact SHA and branch pinned;
- schema identified;
- immutable image digests retained;
- deployment workflow bound to exact candidate;
- required provider permissions verified;
- no unauthorised permission/effect present;
- live signed-in paths accepted;
- monitoring and rollback evidence retained.

## 11.4 Production gate

- QA recommendation green;
- Trust recommendation green or residual risk explicitly accepted;
- operational evidence complete;
- customer/support readiness complete;
- Founder approval recorded;
- exact revision and environment change approved.

# 12. Database and migration rules

- PostgreSQL remains the authoritative persistence store.
- Migrations are append-only, deterministic and checksummed.
- Drift fails closed.
- Migration execution uses advisory locking and a durable ledger.
- A customer slice should normally use no more than one migration.
- Rollback must account for the schema’s compatibility and data-loss implications.
- Release evidence records the exact schema version applied.

# 13. Configuration and secrets

- Browser and server configuration boundaries remain explicit.
- Secrets never enter client-capable code, logs, queue envelopes or artefacts.
- Azure access should use managed identity/OIDC and least privilege.
- Provider registration or subscription-level setup must not be solved by permanently widening the resource-group-scoped deployment identity.
- Feature flags default off for consequential or next-slice capability.
- Controlled-principal gates require exact tenant/object binding where specified.

# 14. Deployment and rollback

A deployment must:

- verify exact revision and environment;
- build or select immutable images;
- verify database readiness and migration ledger;
- verify web/API/worker readiness;
- verify supported identity and connector boundaries;
- retain evidence without customer content;
- fail closed on mismatch.

Rollback must:

- identify the exact prior image digests and compatible schema;
- preserve data integrity;
- restore default-off feature state where required;
- avoid leaving partially activated permissions or secrets;
- be tested/evidenced before production approval.

# 15. Monitoring and incident readiness

Release readiness requires evidence for:

- service availability and readiness;
- queue health, retries and dead letters;
- database connectivity and migration state;
- authentication/membership resolution;
- Microsoft connector health;
- workflow success/failure counts without source content;
- correlation across web/API/worker;
- alert ownership and escalation;
- safe degradation and recovery.

No monitoring design may log email, calendar, draft or customer-knowledge content merely to ease debugging.

# 16. Release freeze and repinning

While #109 controls acceptance:

- the pinned release-candidate SHA remains immutable;
- later `main` changes are not included automatically;
- a proven P0 defect may trigger a corrected candidate;
- a repin must identify the exact new SHA, schema and reason;
- all affected assurance and deployment evidence must be repeated;
- #154 cannot enter the candidate merely because its code is merged behind a flag.

# 17. Post-release review

After a controlled production release, review:

- activation and time to first useful work;
- workflow quality and edit burden;
- support volume and implementation effort;
- incidents, permission concerns and unexpected effects;
- performance, reliability and cost;
- rollback/recovery effectiveness;
- customer value and willingness to pay;
- whether next-slice activation is justified.

Record lessons as issues and update canonical specifications rather than relying on chat recollection.

# 18. Related documents

- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Test and Evaluation Specification](test-evaluation-specification.md)
- [TMOS System Architecture](../architecture/tmos-system-architecture.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md)
- [Cross-Repository Baseline Manifest](../governance/cross-repository-baseline-manifest.md)
- [Delivery Operating Model](../governance/delivery-operating-model.md)