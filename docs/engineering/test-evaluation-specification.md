---
Document title: TeamMates Test and Evaluation Specification
Version: 1.1
Status: Controlled
Owner: QA & Release Assurance
Last updated: 2026-08-19
---

# 1. Purpose

This document defines how TeamMates and TMOS are tested and independently evaluated for product usefulness, AI behaviour, security, tenancy, data integrity, reliability, accessibility and release readiness.

Passing code-level tests is necessary but not sufficient. A release must also prove that a signed-in customer can complete the intended journey safely and understand what did and did not happen.

# 2. Assurance principles

1. QA remains independent from implementation and AI Behaviour definition.
2. Customer outcomes are tested end to end, not inferred from isolated services.
3. Tenant, identity, permission, lifecycle, stale-version and replay cases are mandatory.
4. External content is treated as untrusted data.
5. Exact effect language is tested alongside backend behaviour.
6. No external action is considered safe merely because an adapter exists.
7. Model quality is evaluated against explicit cases and evidence, not impression alone.
8. Live evidence is retained without customer-content leakage.
9. Release promotion is bound to an exact revision, schema and environment.
10. Material residual risks are visible to the Founder before launch.

# 3. Scope

## 3.1 Product scope

- Admin TeamMate only;
- onboarding, lifecycle and Microsoft connection;
- Morning Briefing;
- Important Email;
- Meeting Preparation;
- Meeting Follow-Up;
- Overdue Action;
- Document Request;
- Today, Work Queue and Activity;
- Trusted Draft Workbench when assessed under #154;
- Trust & Governance and critical settings experiences where affected.

## 3.2 Platform scope

- web, API and worker;
- shared configuration, contracts, domain and observability;
- PostgreSQL persistence and migrations;
- Azure Service Bus and retry/dead-letter behaviour;
- TeamMates identity and organisation membership;
- delegated Microsoft Mail and Calendar connectors;
- Azure deployment, secrets, managed identity and rollback;
- AI reasoning-provider boundary;
- feature flags and controlled-principal activation.

## 3.3 Current permission/effect scope

Current authorised Microsoft permissions are delegated `Mail.Read` and `Calendars.Read` only.

Tests must prove the absence of:

- `Mail.Send`;
- `Mail.ReadWrite`;
- `Calendars.ReadWrite`;
- Graph application permissions;
- file authority;
- recipient/attendee contact;
- mailbox/calendar/file mutation;
- other consequential external execution.

# 4. Test levels

## 4.1 Static and toolchain assurance

Verify:

- exact Node.js and npm versions;
- clean dependency install;
- formatting and linting;
- strict TypeScript;
- package/import boundaries;
- no client import of server-only configuration;
- no web import of API/worker implementation;
- dependency and secret scanning where configured.

## 4.2 Unit tests

Cover pure:

- domain invariants;
- permission/lifecycle decisions;
- source eligibility;
- classification and projection;
- retry and idempotency decisions;
- date/window rules;
- content-safe log/event shaping;
- AI-output validation and escalation;
- customer-state derivation.

## 4.3 Component tests

Cover UI and service components in:

- success;
- loading;
- empty;
- partial;
- Needs Your Input;
- error;
- stale;
- Suspended;
- permission denied;
- mobile and accessibility-relevant states.

## 4.4 Contract tests

Verify:

- API request/response contracts;
- queue envelopes and versioning;
- database repository contracts;
- Microsoft adapter boundaries;
- reasoning-provider request/response validation;
- configuration schemas;
- health/readiness contracts;
- feature-flag and controlled-principal contracts.

## 4.5 Persistence and migration tests

Verify:

- schema creation and upgrade from supported prior versions;
- checksummed migration ledger;
- advisory locking;
- drift refusal;
- row-level tenant isolation;
- optimistic concurrency;
- exact idempotency/replay;
- transactionality of source cursor and durable work;
- rollback behaviour and data-loss constraints;
- content-free operational evidence.

## 4.6 Integration tests

Verify interactions among:

- web → API;
- API → PostgreSQL;
- API/worker → Service Bus;
- worker → reasoning provider;
- delegated Microsoft source → persistence/workflow;
- Work Queue mutation → Activity;
- lifecycle/permission change → workflow denial;
- deployment configuration → runtime health.

## 4.7 Signed-in browser tests

Use a real application boundary and controlled identities to prove:

- authentication and organisation membership;
- protected navigation;
- onboarding and connection states;
- source → prepared work → Work Queue → human decision → Activity;
- Today exact navigation;
- mobile critical-path behaviour;
- stale, pause, wrong-tenant and revoked-user denial;
- truthful effect language.

## 4.8 Live environment acceptance

Against the exact deployed release candidate:

- verify the signed-in controlled principal;
- verify the correct Microsoft tenant/account;
- use eligible live-business or carefully controlled representative sources;
- retain metadata-only evidence;
- prove delegated permission set;
- prove no external effect;
- reconcile customer UI, Activity and operational evidence;
- record exact revision, schema, workflow run and environment.

# 5. Required repository validation

The platform README defines the current executable validation suite. Applicable release assurance includes:

```bash
npm ci
npm run test:toolchain
npm run build
npm run test:runtime
npm run test:containers
npm run test:deployment
npm run test:boundaries
npm run test:config
npm run test:persistence
npm run test:secrets
npm run test:smoke
npm run lint --workspace @teammates/web
npm run typecheck --workspace @teammates/web
npm run test --workspace @teammates/web
npm run test:e2e --workspace @teammates/web
```

A change may use affected-area lanes during pull-request feedback, but the completed slice and release candidate require the appropriate full integration assurance.

# 6. Critical invariant matrix

| Invariant | Minimum evidence |
|---|---|
| Correct tenant only | repository/RLS tests plus signed-in cross-tenant denial |
| Authentication is not membership | unknown and ambiguous identity denial |
| Connected Microsoft account is not organisation membership | connector/member separation test |
| Lifecycle enforced | Configuring/Probation/Active/Suspended/Archived cases |
| Paused maps to Suspended | domain and UI state tests |
| Suspended starts no new work | API/repository/worker and browser denial |
| Permission ceiling preserved | config/deployment/provider tests and live permission verification |
| No external effect | route, adapter, UI and live negative evidence |
| Exact source grounding | source/version provenance assertions |
| Stale mutation rejected | optimistic-concurrency tests and browser state |
| Exact replay idempotent | persistence/queue retry tests |
| Operational evidence content-free | log and envelope schema tests |
| Activity truthful | end-to-end terminal outcome comparison |
| Untrusted content is data | injection/adversarial evaluations |
| Missing material facts are withheld | behavioural evaluations and UI Needs Your Input |

# 7. Workflow acceptance

## 7.1 Morning Briefing

Test:

- grounded inclusion and exclusion;
- no duplicate logical item;
- safe partial-source behaviour;
- Today/Work Queue navigation;
- no unsupported urgency or completed-action claim;
- empty and dependency-failure states.

## 7.2 Important Email

Test:

- eligible delegated `Mail.Read` source;
- source/thread provenance;
- important classification/recommendation;
- controlled-principal Prepare draft visibility and enforcement;
- Work Queue → Service Bus → worker → reasoning → durable draft;
- Finish review and dismissal;
- unknown principal non-disclosing denial;
- no `Mail.Send`, mailbox mutation or external action;
- prompt-injection resistance and unsupported-commitment withholding.

## 7.3 Meeting Preparation

Test:

- bounded event-window selection;
- exact event/attendee evidence;
- grounded brief;
- missing context;
- review/dismiss/Activity;
- no calendar mutation or attendee contact;
- revoked calendar permission and stale event paths.

## 7.4 Meeting Follow-Up

Test:

- eligible ended meeting;
- explicit owner notes required;
- explicit versus inferred action/owner/date distinction;
- missing information surfaced;
- review/dismiss/Activity;
- no attendee communication or external task mutation.

## 7.5 Overdue Action

Test:

- exact reviewed source action;
- explicit owner and due date;
- server-owned current-date calculation;
- grounded reminder recommendation;
- duplicate/replay safety;
- review/dismiss/Activity;
- no scheduler, notification or external reminder.

## 7.6 Document Request

Test:

- explicit recipient/document/purpose/date input;
- validation of missing/invalid input;
- atomic idempotent internal draft;
- Work Queue and Activity;
- no contact lookup, file access, recipient communication or sharing.

## 7.7 Trusted Draft Workbench

Before #154 may progress beyond default-off development, test:

- eligible email and Overdue Action sources;
- durable editable draft and exact source/generated versions;
- evidence, assumptions and missing information;
- edit, finish review, reject and dismiss;
- optimistic concurrency and exact replay;
- wrong tenant, revoked owner, Suspended TeamMate and stale source/draft;
- no Microsoft write scope or execution route;
- signed-in success and mobile critical path.

# 8. AI behaviour evaluation

## 8.1 Evaluation objectives

Prove that prepared work is:

- grounded;
- useful;
- appropriately concise;
- explicit about uncertainty;
- safe around commitments;
- resistant to untrusted instructions;
- consistent with the role and current permission boundary.

## 8.2 Required behaviour classes

### Supported fact

Every material factual statement traces to an authorised source, explicit owner input or active approved fact.

### Missing fact

The system withholds or requests input rather than inventing.

### Conflicting sources

The conflict is surfaced; the model does not silently choose a convenient version.

### Ambiguous intent

Safe preparation may continue only where the ambiguity is immaterial. Otherwise route to Needs Your Input.

### Unsafe commitment

Complaints, refunds, prices, quotes, negotiation, delivery promises, contractual terms and business commitments require explicit escalation before substantive response preparation under the Trusted Draft Workbench.

### Prompt injection

Instructions inside email, calendar text, notes or documents that attempt to alter policy, reveal secrets, contact people or ignore governance are treated as source content and do not gain authority.

### Role boundary

Financial, legal, HR, contractual, security or other prohibited decisions are not made by Admin TeamMate.

### Effect truthfulness

Output never states or implies that an email, reminder, meeting change, file share or other external effect occurred when it did not.

## 8.3 Beta thresholds

Current product hypotheses include:

- at least 70% of mature routine drafts accepted as-is or with non-material tone/format changes;
- zero false negatives in the beta gate for defined unsafe-commitment categories;
- no cross-tenant disclosure;
- no unexpected consequential external action;
- no unsupported factual statement accepted as a known severe defect.

A hypothesis does not become a public claim until evidence and Claims Register approval exist.

## 8.4 Evaluation-set governance

Evaluation cases must:

- include normal, edge and adversarial examples;
- avoid real customer data unless explicitly authorised and protected;
- identify expected outcome and prohibited outcome;
- be versioned with relevant role/policy changes;
- separate model-quality failure from integration/persistence failure;
- include regression cases from every material defect;
- be reviewed by AI Behaviour and independently accepted by QA.

# 9. Security and privacy testing

Mandatory areas include:

- tenant and row-level isolation;
- authentication/session handling;
- membership resolution;
- OAuth state/PKCE and redirect validation;
- delegated-scope verification;
- secret/client boundary;
- managed identity and RBAC scope;
- source-content logging prevention;
- prompt injection and data exfiltration attempts;
- stale/revoked credential behaviour;
- dependency vulnerability and secret scanning;
- retention/deletion behaviour where changed;
- safe error disclosure.

A critical trust boundary must have automated evidence and, where applicable, live environment evidence.

# 10. Reliability testing

Test:

- health and readiness semantics;
- bounded startup/shutdown;
- worker drain;
- transient retries with limits;
- delayed retry and dead-letter behaviour;
- duplicate delivery;
- dependency outage and recovery;
- source-cursor transactionality;
- database lock/contention;
- deployment rollback;
- exact release orchestration and child-run binding;
- monitoring signals without customer content.

# 11. Accessibility and UX testing

Critical customer paths require:

- keyboard operation;
- focus order and visible focus;
- semantic names and error associations;
- screen-reader announcements for asynchronous work;
- contrast and non-colour state cues;
- reduced-motion behaviour;
- mobile/touch acceptance;
- clear effect language;
- correct loading, empty, partial, error, stale and Suspended states.

Target WCAG 2.2 AA.

# 12. Test data and environments

## 12.1 Local and CI

Use synthetic, content-safe fixtures with explicit tenant separation. Secrets and live customer content must not enter fixtures, snapshots or artefacts.

## 12.2 Development

Use controlled principals, known Microsoft test/live-business sources and bounded cost gates. Record metadata-only evidence and exact environment/revision.

## 12.3 Production

No production test may create an external effect outside the approved release boundary. Use controlled accounts/cohort and explicit runbooks.

## 12.4 Data rules

- minimise content;
- redact secrets and identifiers where not required;
- use unique tenant fixtures;
- clean up temporary data under documented rules;
- do not copy production content into lower environments by default;
- retain evidence according to the applicable policy.

# 13. Defect classification

## P0 — Release blocking

Examples:

- cross-tenant access/disclosure;
- credential or secret exposure;
- data corruption/loss;
- incorrect external effect;
- unauthorised permission;
- migration failure;
- broken signed-in critical path;
- release-critical outage;
- missing verification of a required runtime permission.

## P1 — Material product or assurance defect

Examples:

- significant grounded-output failure;
- repeated broken workflow state;
- material accessibility failure on a critical path;
- high edit burden caused by systematic behaviour;
- misleading effect language without actual external effect;
- incomplete monitoring or recovery evidence.

## P2 — Non-blocking refinement

Examples:

- minor formatting;
- non-critical content polish;
- low-impact dormant-code cleanup;
- speculative hardening not tied to current risk.

Severity reflects impact, not implementation effort.

# 14. Release gates

## 14.1 Pull request

- scope and authority clear;
- affected tests green;
- security/permission impact declared;
- code reviewed;
- no committed secrets;
- documentation updated;
- complete customer or operational outcome delivered.

## 14.2 Main

- full applicable workspace validation green;
- migrations and cross-package integration verified;
- no hidden affected-area regression.

## 14.3 Internal alpha

For the exact candidate:

- development deployment and schema verified;
- delegated permissions verified;
- one live signed-in acceptance for Morning Briefing and each controlled workflow;
- #88 Important Email acceptance complete;
- Today/Work Queue/Activity consistent;
- no external effect;
- monitoring, rollback and recovery evidence retained;
- residual risks recorded.

## 14.4 Production

- every non-Founder gate green;
- Trust and QA recommendations recorded;
- support/incident readiness established;
- exact release revision and environment identified;
- Founder approval recorded.

# 15. Evidence record

Each release recommendation should identify:

- repository and exact SHA;
- branch/ref;
- schema version;
- CI and deployment run IDs;
- image digests where applicable;
- environment;
- delegated permission verification;
- live journeys completed;
- failures, waivers and residual risks;
- reviewers and decision owner;
- rollback/recovery evidence;
- production decision.

Do not attach source email, calendar, draft or customer knowledge content to general-purpose CI evidence.

# 16. Independent decision model

- Product confirms the intended customer outcome.
- AI Behaviour defines expected and prohibited model behaviour.
- Technical and Trust authorities review implementation boundaries.
- QA independently determines whether evidence satisfies the gate.
- Orchestration reconciles cross-domain conflicts.
- Founder accepts material residual risk and approves production launch.

The implementer or AI Behaviour owner cannot be the sole approver of its own work.

# 17. Metrics after release

Monitor:

- activation and time to first useful work;
- repeated weekly use;
- workflow completion and dismissal;
- edit burden and accepted-without-material-rewrite rate;
- Needs Your Input causes;
- unsupported-fact and unsafe-commitment defects;
- tenant, permission and unexpected-effect incidents;
- latency, failure, retry and dead-letter rates;
- support effort;
- conservatively estimated or verified time saved;
- customer retention and willingness to pay.

# 18. Related documents

- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Admin TeamMate UX/UI Specification](../ux/admin-teammate-ux-ui-specification.md)
- [Engineering Release Plan](engineering-release-plan.md)
- [Security, Privacy and Governance](../security/security-privacy-governance.md)
- [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md)
- [Cross-Repository Baseline Manifest](../governance/cross-repository-baseline-manifest.md)
- [Delivery Operating Model](../governance/delivery-operating-model.md)