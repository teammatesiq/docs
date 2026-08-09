---
Document title: Admin TeamMate MVP Sprint Plan
Version: 1.0
Status: Approved
Owner: TeamMates
Last updated: 2026-08-09
---

# 1. Purpose

This plan converts the approved TeamMates / TMOS Specification Baseline v1.0 into an executable sprint sequence for building the Admin TeamMate SME MVP.

The plan is deliberately organised around working vertical slices. It does not create new product scope, alter the canonical lifecycle, or treat internal demonstrations as beta readiness.

# 2. Delivery outcome

Build a controlled-beta product in which a UK SME can:

1. sign in and create an organisation;
2. deploy Admin TeamMate;
3. connect an authorised Microsoft 365 account;
4. complete onboarding and enter Probation;
5. receive useful work from live authorised information;
6. review work in a durable Work Queue;
7. approve a controlled email action;
8. receive a Daily Briefing;
9. use approved knowledge, meeting, action and document workflows;
10. understand, pause and govern the TeamMate; and
11. see a truthful measure of value delivered.

Project TeamMate, Microsoft Contacts, multi-TeamMate orchestration and the other exclusions in the baseline remain outside this plan.

# 3. Planning assumptions

| Assumption | Planning basis |
|---|---|
| Sprint length | Two weeks |
| Build team | One senior full-stack engineer and one AI/backend engineer |
| Supporting capacity | Founder/Product Owner; product designer at approximately 0.5 FTE; security/cloud support at approximately 0.2 FTE |
| Planned engineering capacity | 70% committed backlog; 20% tests, defects and hardening; 10% operational work and uncertainty |
| Delivery model | Trunk-based development with short-lived branches and pull requests |
| Architecture | Next.js/React/TypeScript frontend; TypeScript modular-monolith backend; PostgreSQL/pgvector; asynchronous workers and managed queue |
| First integrations | Microsoft Entra ID, Exchange Online, Calendar, SharePoint and OneDrive; no Microsoft Contacts scopes |
| Environments | Local, development, staging and production, with production isolated from non-production |
| Release method | Feature flags, automated deployment, observable changes and rollback |

The target is **12 sprints / 24 delivery weeks** for controlled-beta readiness. This is an evidence-based forecast, not a fixed promise. With one engineer, the likely duration increases materially; with three experienced engineers and timely provider access, selected workstreams can overlap but the trust gates cannot be skipped.

This cadence and the two-engineer planning basis were approved by the Product Owner on 9 August 2026.

# 4. Milestones

| Milestone | Target | Demonstrable outcome |
|---|---:|---|
| M1 — Running foundation | End Sprint 1 | Application deploys automatically to development with health, CI and initial authenticated shell |
| M2 — Secure platform foundation | End Sprint 2 | Identity, tenant isolation, database migrations, audit and outbox pass automated gates |
| M3 — First useful TeamMate | End Sprint 4 | Alex is deployed, connected to Microsoft 365 and prepares one useful work item from live authorised data |
| M4 — Trusted work loop | End Sprint 6 | Important Email can proceed from event to draft, approval, idempotent Microsoft send, confirmation and audit |
| M5 — Functional Admin TeamMate | End Sprint 10 | Six approved capabilities are usable through governed workflows and Ask Alex |
| M6 — Controlled SME beta | End Sprint 12 | Security, quality, operational, support, billing, analytics and beta-readiness gates pass |

# 5. Workstreams

Each sprint should move the following workstreams together rather than leaving security, UX or evaluation to the end:

- **Product and UX:** thin, complete customer journeys with responsive and accessible behaviour.
- **Platform and data:** tenancy, domain records, events, workflows, audit, migrations and operations.
- **Microsoft integration:** OAuth, Graph contracts, health, events, retries, disconnection and provider confirmation.
- **AI and evaluation:** versioned prompts, structured outputs, grounding, uncertainty, injection resistance and regression datasets.
- **Trust and security:** permissions, protected policy, approvals, re-evaluation, idempotency, lifecycle controls and audit reconstruction.
- **Quality and release:** automated tests, observability, deployment, rollback and release evidence.

# 6. Sprint roadmap

## Sprint 1 — Working application skeleton

**Goal:** Put production-shaped code into a development environment and establish the delivery path.

**Committed scope:**

- create the application workspace and modular package boundaries;
- scaffold responsive web, API and worker applications;
- configure linting, formatting, type checking and automated tests;
- implement environment configuration and secrets boundaries;
- create health/readiness endpoints, request IDs and structured error handling;
- establish automated development deployment and rollback procedure;
- implement the sign-in screen and authenticated application shell behind a feature flag;
- record only the provider ADRs required to build safely, in parallel with scaffolding.

**Sprint demo:** A user opens the development URL, signs in through the configured development identity route, reaches the empty TeamMates shell and engineering can trace the request through logs.

**Exit evidence:** Reproducible build; green CI; no committed secret; development deployment from `main`; smoke test and rollback test pass.

**Baseline traceability:** E0.1, part of E0.2; NFR-003, NFR-009.

## Sprint 2 — Identity, tenancy and durable foundations

**Goal:** Prove the platform can safely separate organisations before customer data or AI work is introduced.

**Committed scope:**

- complete Microsoft-compatible authentication, sessions, logout and expiry;
- implement organisations, users, membership and default workspace;
- establish server-owned tenant resolution and tenant-aware repositories;
- introduce PostgreSQL RLS where specified;
- create the initial domain migrations, including Blueprint, TeamMate, Task, Workflow, Approval and governance records;
- implement append-only audit events;
- implement the standard event envelope, transactional outbox and publisher worker;
- automate cross-tenant, migration and outbox failure tests.

**Sprint demo:** Two test organisations use the same deployment without accessing each other's records; an organisation change creates an auditable, atomically published event.

**Exit evidence:** Release 0 criteria pass, including 100% of mandatory tenant-isolation checks and repeatable staging migrations.

**Baseline traceability:** E0.2–E0.6; Quality Gates 80 and 82.

## Sprint 3 — Deploy Alex and complete governed setup

**Goal:** Allow an SME user to deploy Alex through the approved Configuring journey.

**Committed scope:**

- seed the Admin TeamMate Role and immutable Released Blueprint composition;
- implement one-TeamMate deployment and customer display name;
- implement Configuring lifecycle and server-owned transition readiness;
- build organisation setup, Meet Alex, permission education and business introduction;
- implement permission definitions, assignments, role restrictions and effective permission summary;
- implement protected platform policy and tenant policy precedence;
- persist onboarding progress, preferences and setup summary;
- add Blueprint immutability, permission precedence and lifecycle-authorisation tests.

**Sprint demo:** A user creates an organisation, deploys Alex, understands the proposed authority and resumes an interrupted setup without losing progress.

**Exit evidence:** Deployed Alex can be reconstructed from the exact Released Blueprint; permissions are enforced server-side; no client can directly start Probation.

**Baseline traceability:** E1.1, E1.3–E1.5; Journey A up to Microsoft connection.

## Sprint 4 — Microsoft connection and first useful live work

**Goal:** Deliver the first genuine customer-value vertical slice using authorised Microsoft data.

**Committed scope:**

- implement Microsoft OAuth state, callback, protected credential storage, granted-scope validation and disconnection;
- implement Mail read and Calendar read through provider-neutral contracts;
- expose connection health and safe repair states;
- implement Runtime and Reasoning Service interfaces with versioned prompts and structured outputs;
- persist AI-run traceability and usage metadata;
- implement Microsoft event ingestion and deduplication;
- implement Important Email classification and draft preparation without external send;
- complete internal readiness validation and Configuring → Probation transition;
- measure time to first useful live work.

**Sprint demo:** Alex enters Probation, reads authorised Microsoft data and prepares a sourced draft or calendar insight from live information. Nothing is externally sent.

**Exit evidence:** Release 1 criteria pass; duplicate event is safe; no Contacts scope is requested; failed AI calls cannot corrupt workflow state.

**Baseline traceability:** E1.2, E1.6–E1.10; WF-ADM-002; Journey A.

## Sprint 5 — Work Queue and approval controls

**Goal:** Make prepared work durable, reviewable and controllable.

**Committed scope:**

- implement Work Queue and customer state mapping;
- implement work detail, evidence, confidence and source context;
- implement the Approval domain object;
- support approve, reject, amend, defer and expiry;
- preserve proposal, assumptions, amendments and final approved action;
- implement Needs Your Input and durable resume;
- implement cancellation and visible timeout behaviour;
- automate replay, stale-control, amendment and audit-reconstruction tests.

**Sprint demo:** An email draft appears in Ready For You, can be amended or rejected, and retains a complete immutable decision history through restart.

**Exit evidence:** No rejected, expired or mismatched approval can reach execution; current Work Queue state survives API and worker restart.

**Baseline traceability:** E2.1–E2.3, E2.7–E2.8; Journey D.

## Sprint 6 — Controlled email send and Daily Briefing

**Goal:** Complete the core trust hypothesis and establish a useful daily return journey.

**Committed scope:**

- re-evaluate permission, policy and approved action immediately before execution;
- implement idempotent Microsoft email send;
- distinguish Submitted to Microsoft from provider-confirmed completion;
- reconcile indeterminate provider outcomes without blind retry;
- implement WF-ADM-001 Daily Briefing scheduling and generation;
- build Today with priority, approvals, meetings and action summary;
- add safe partial-failure presentation;
- implement initial probation-progress evidence.

**Sprint demo:** One incoming email travels end to end from Microsoft event to draft, human approval, single provider-confirmed send, audit and value record; the next Daily Briefing reflects current state.

**Exit evidence:** Release 2 trusted-email gate passes with no manual database intervention; controlled external-action idempotency and workflow-durability suites pass.

**Baseline traceability:** E2.4–E2.6, E2.9; WF-ADM-001 and WF-ADM-002; Journey B.

## Sprint 7 — Governed organisational knowledge

**Goal:** Ground Alex in customer-selected SharePoint, OneDrive and uploaded sources without crossing access boundaries.

**Committed scope:**

- implement source selection, status and disconnect;
- implement asynchronous retrieval, extraction, chunking, embedding and indexing;
- preserve source, version, checksum, classification and access metadata;
- implement pgvector retrieval with tenant, workspace, source and classification filtering;
- display source references and partial-indexing failures;
- add prompt-injection and indirect prompt-injection controls at ingestion and use;
- automate disconnected-source and cross-tenant retrieval tests.

**Sprint demo:** A user selects a bounded source, sees its sync state and receives a sourced answer; another organisation and a disconnected source are provably inaccessible.

**Exit evidence:** Knowledge quality gate passes, including 100% of cross-tenant and disconnected-source cases.

**Baseline traceability:** E3.1–E3.3; WF-PLT-002.

## Sprint 8 — Meetings and action management

**Goal:** Turn authorised meeting context into preparation and traceable follow-through.

**Committed scope:**

- implement WF-ADM-003 Meeting Preparation;
- implement WF-ADM-004 Meeting Follow-Up;
- distinguish explicit actions from inferred actions;
- implement the versioned Action Task profile and Action Register;
- support missing owner/date without fabrication;
- implement WF-ADM-005 Overdue Action with duplicate-safe reminder control;
- add the meeting and action evaluation datasets and UAT journey.

**Sprint demo:** Alex prepares a sourced meeting brief, processes supplied notes, records decisions/actions and proposes an approval-controlled follow-up.

**Exit evidence:** Journey C passes; conflicting evidence is visible; repeat reminders cannot spam recipients.

**Baseline traceability:** E3.4–E3.7; WF-ADM-003, WF-ADM-004 and WF-ADM-005.

## Sprint 9 — Documents, Ask Alex and governed learning

**Goal:** Complete the remaining approved Admin TeamMate capabilities and direct-delegation path.

**Committed scope:**

- implement WF-ADM-006 for the approved routine-document types;
- enforce evidence-backed claims and Needs Your Input for missing material facts;
- implement Ask Alex as a cross-cutting route into governed Tasks and Workflows;
- implement learning proposals, confirm, reject, defer and preference removal;
- prevent learning from changing permissions, policy or integration scope;
- implement writing tone, sign-off, priority-contact preference and briefing preference learning;
- add document, unsupported-request and learning-safety evaluation cases.

**Sprint demo:** A user asks Alex for an in-scope document, supplies a missing fact through Needs Your Input, receives a traceable draft and confirms or rejects a separate preference proposal.

**Exit evidence:** Conversation is not the work system of record; learning authority tests pass; unsupported work is refused or redirected truthfully.

**Baseline traceability:** E3.8–E3.10; WF-ADM-006 and WF-PLT-004; Journey D.

## Sprint 10 — Trust, lifecycle and value surfaces

**Goal:** Make the functional pilot understandable, governable and measurable by the customer.

**Committed scope:**

- complete Trust & Governance surfaces for TeamMate, permissions, integrations, knowledge, approvals, audit and learning;
- implement Pause as `suspended/customer_paused`, Resume and all canonical non-customer suspension labels;
- ensure suspension stops new work and controlled external action while preserving required state;
- implement reactivation validation for entitlement, integration, permissions, policy and configuration;
- implement probation review and explicit completion without authority expansion;
- implement Value Events, Trusted Work Completed and conservative estimated-time-saved summaries;
- complete mobile-first review/approval and core accessibility remediation.

**Sprint demo:** The customer can explain what Alex can access and do, pause and resume Alex, review audit evidence, complete Probation without gaining authority and see truthful value delivered.

**Exit evidence:** Release 3 functional-pilot criteria pass; lifecycle, suspension and probation-authority regression suites pass.

**Baseline traceability:** E3 exit; E4.2, E4.4 and part of E4.8; Journey E.

## Sprint 11 — Commercial and operational readiness

**Goal:** Make the product operable and commercially testable without weakening the trust controls.

**Committed scope:**

- implement the 14-day trial hypothesis and Stripe subscription/entitlement boundary;
- implement authenticated and idempotent billing webhooks;
- implement trial-expiry and billing-suspension reasons plus recovery routes;
- implement activation, first-value, repeat-use and conversion analytics;
- implement support tooling that avoids routine mailbox/document content access;
- add API/workflow/provider health, queue depth, retry, cost and security observability;
- configure alerts, incident route, backups, restore exercise and deployment rollback;
- prepare onboarding/support material for design partners.

**Sprint demo:** A test organisation can enter trial, use Alex, expire into the correct suspension reason, recover through billing and be diagnosed operationally without raw database access.

**Exit evidence:** Operational-readiness checklist passes; dashboard and alerts identify a seeded failed workflow; backup restore and rollback are evidenced.

**Baseline traceability:** E4.3, E4.5–E4.7.

## Sprint 12 — Beta hardening and release evidence

**Goal:** Prove the system is safe, useful, supportable and ready for 5–10 controlled design partners.

**Committed scope:**

- complete threat model and security/privacy review;
- complete dependency, secret, session, OAuth, webhook, rate-limit and input-validation hardening;
- run tenant-isolation, approval, idempotency, workflow-durability and audit-reconstruction suites;
- run the golden AI dataset, prompt regression, model regression and red-team scenarios;
- complete WCAG 2.2 AA checks for P0 journeys and practical mobile approval;
- run UAT Journeys A–E in staging with synthetic SME data;
- resolve all Critical and High defects and document treatment of remaining defects;
- rehearse customer onboarding, support, pause, integration repair, incident response and rollback;
- hold the formal beta-readiness review.

**Sprint demo:** A release candidate completes every P0 journey under observed staging conditions, including seeded failure and recovery scenarios.

**Exit evidence:** Release 4 gate passes; zero unresolved Critical/High risks or defects; required security, privacy, AI, operational and customer-readiness approvals are recorded.

**Baseline traceability:** E4.1, E4.8 and Release 4 exit; Test Specification release gate.

# 7. Baseline epic coverage

| Baseline release | Epics | Planned sprint |
|---|---|---|
| Release 0 | E0.1 Repository and Application Foundation | Sprint 1 |
| Release 0 | E0.2 Authentication | Sprints 1–2 |
| Release 0 | E0.3 Organisation and Tenancy; E0.4 Core Database Foundation; E0.5 Audit Foundation; E0.6 Domain Events and Outbox | Sprint 2 |
| Release 1 | E1.1 TeamMate Blueprint and Deployment; E1.3 Permission Engine; E1.4 Policy Foundation; E1.5 Onboarding | Sprint 3 |
| Release 1 | E1.2 Microsoft 365 Integration; E1.6 TeamMate Runtime Foundation; E1.7 AI Reasoning Service; E1.8 Integration Event Ingestion; E1.9 Important Email Preparation; E1.10 First Live Value | Sprint 4 |
| Release 2 | E2.1 Work Queue; E2.2 Approval Engine; E2.3 Approval Resume; E2.7 Needs Your Input; E2.8 Cancellation and Timeouts | Sprint 5 |
| Release 2 | E2.4 Email Send; E2.5 Daily Briefing Workflow; E2.6 Today Experience | Sprint 6 |
| Release 2 | E2.9 Probation Progress | Sprints 6 and 10 |
| Release 3 | E3.1 Knowledge Source Management; E3.2 Knowledge Ingestion; E3.3 Permission-Aware Knowledge Search | Sprint 7 |
| Release 3 | E3.4 Meeting Preparation; E3.5 Meeting Follow-Up; E3.6 Action Register; E3.7 Overdue Action Workflow | Sprint 8 |
| Release 3 | E3.8 Document Request Workflow; E3.9 Learning; E3.10 Ask Alex | Sprint 9 |
| Release 4 | E4.2 Trust & Governance; E4.4 Value Measurement | Sprint 10 |
| Release 4 | E4.3 Observability; E4.5 Billing and Trial; E4.6 Product Analytics; E4.7 Support Tooling | Sprint 11 |
| Release 4 | E4.1 Security Hardening | Sprint 12 |
| Release 4 | E4.8 UX and Accessibility Polish | Sprints 10–12 |

Every release-plan epic is represented. Sprint placement does not weaken the epic's canonical acceptance criteria or release gate.

# 8. Critical path

The critical path is:

1. repository and delivery pipeline;
2. identity and tenant isolation;
3. domain migrations, audit and outbox;
4. immutable Admin TeamMate Blueprint and deployment;
5. Microsoft OAuth and provider contracts;
6. permissions and protected policy;
7. Runtime and durable workflow;
8. Important Email preparation;
9. Approval, pre-execution re-check and idempotent send;
10. security and beta release evidence.

Knowledge, UI refinement, evaluation datasets, support preparation and operational tooling should progress alongside this path when their dependencies permit.

# 9. Sprint operating model

## Before each sprint

- Product Owner confirms the customer outcome and priority.
- Engineering refines only enough work for the next sprint plus one sprint ahead.
- Every committed item meets the baseline Definition of Ready.
- Dependencies, security/data impact and required tests are explicit.
- Unresolved product decisions are escalated before commitment.

## During each sprint

- merge small increments behind feature flags;
- run automated checks on every pull request;
- demonstrate integrated software at least weekly;
- evaluate AI behaviour whenever prompt, model, context or tool behaviour changes;
- fix Critical and High defects before adding lower-priority scope;
- update the delivery forecast from evidence, not optimism.

## At sprint review

- demonstrate the end-to-end outcome in the development or staging environment;
- show the test and operational evidence, not slides alone;
- accept or reject against the stated exit evidence;
- update risks, dependencies and milestone forecast;
- move unfinished work back to the backlog rather than silently carrying it as Done.

# 10. Definition of Done

A backlog item is Done only where applicable evidence confirms:

- code is merged and reviewed;
- automated tests pass;
- tenant and permission boundaries pass;
- migrations apply and roll back safely;
- audit and observability are present;
- error, empty, loading and recovery states work;
- responsive and accessibility requirements are met;
- AI evaluation passes for AI-affecting changes;
- acceptance criteria are demonstrated;
- documentation and traceability are updated;
- the change is deployed to the intended environment behind the appropriate flag.

# 11. Release gates

The following are non-negotiable:

- no external customer access until Release 0 controls pass;
- no controlled external email without an Approval object and immediate permission/policy re-evaluation;
- no completion claim for an external action before provider confirmation;
- no release with a known cross-tenant data path;
- no production release with unresolved Critical or High security, AI or trust defects;
- no Probation completion that changes authority;
- no inaccessible or disconnected knowledge in retrieval;
- no beta until monitoring, support, backup, restore and rollback evidence exists.

# 12. Capacity sensitivity

| Delivery capacity | Forecast implication |
|---|---|
| One engineer plus part-time support | Expect approximately 36–44 delivery weeks; integration, platform and workflow work are largely serial |
| Two engineers plus stated support | Plan on 24 delivery weeks; this is the baseline forecast |
| Three experienced engineers plus stated support | Approximately 18–22 delivery weeks may be feasible by overlapping UX, integration, workflow and quality work after Sprint 2 |

Adding people does not compress Microsoft consent lead time, security evidence, AI evaluation or beta observation to zero.

# 13. Immediate mobilisation backlog

The first five working days should produce code and unblock Sprint 1:

1. confirm named Product, Engineering, AI Quality, UX and Security owners;
2. confirm engineering capacity and availability for the first four sprints;
3. confirm the application repository and branch-protection approach;
4. provision development Microsoft Entra tenant/app registration and test mail/calendar accounts;
5. provision development hosting, PostgreSQL, queue, object storage and secrets management;
6. confirm OpenAI project, budget controls and data-handling configuration;
7. scaffold web, API, worker and shared packages;
8. enable CI for build, lint, type check, unit test, secret scan and dependency scan;
9. deploy the first health endpoint and authenticated shell;
10. create Sprint 1 stories with specification links and test obligations.

Access/provisioning work must run in parallel with repository scaffolding. Missing provider access should not prevent local code, contracts, migrations or automated tests from starting.

# 14. Initial delivery risks

| Risk | Early treatment | Owner |
|---|---|---|
| Microsoft tenant, OAuth consent or webhook setup delays | Provision in Sprint 1; use contract fakes only for automated tests, never as release evidence | Engineering |
| Tenant isolation defect | Central tenant context, RLS where specified and blocking cross-tenant tests from Sprint 2 | Engineering/Security |
| AI output appears useful but is ungrounded | Versioned structured outputs, source evidence and golden dataset from first AI slice | AI Quality |
| Duplicate or uncertain Microsoft send | Approval binding, idempotency, provider confirmation and reconciliation before external send | Engineering/Security |
| UX is built ahead of real state | Bind UI to durable backend state; no fake progress or prototype-only state in release demos | Product/UX |
| Scope expands beyond Admin TeamMate | Require specification traceability; route other TeamMates and deferred capabilities to post-MVP backlog | Product Owner |
| Hardening is deferred to the final sprint | Apply security, observability and evaluation work in every sprint; Sprint 12 proves rather than invents controls | Engineering/Security/QA |
| Small team becomes a single point of failure | Document runbooks and service boundaries; pair on critical tenancy, approval and Microsoft code | Engineering |

# 15. Decision and change control

This plan may be reforecast as evidence emerges. A change requires product approval where it alters:

- MVP scope or capability;
- customer-visible lifecycle or permissions;
- a release gate;
- controlled external-action behaviour;
- beta entry criteria; or
- the target milestone by more than one sprint.

Technical implementation choices may evolve through ADRs where they preserve the approved product, trust and architecture boundaries.

# 16. Canonical references

- [Product Requirements](../../docs/strategy/product-requirements.md)
- [Engineering Release Plan and MVP Backlog](../../docs/engineering/engineering-release-plan.md)
- [Platform Architecture](../../docs/architecture/tmos-platform-architecture.md)
- [Data Model and Database Schema](../../docs/engineering/data-model-database-schema.md)
- [API Contract and Service Interfaces](../../docs/engineering/api-contract-service-interfaces.md)
- [Admin TeamMate Workflows](../../docs/product/admin-teammate-workflows.md)
- [Admin TeamMate Onboarding and Probation](../../docs/product/admin-teammate-onboarding-probation.md)
- [Admin TeamMate UX/UI Specification](../../docs/ux/admin-teammate-ux-ui-specification.md)
- [Security, Privacy and Governance](../../docs/security/security-privacy-governance.md)
- [Test and Evaluation Specification](../../docs/engineering/test-evaluation-specification.md)

# 17. Execution backlog

- [Sprint 1 Engineering Backlog](sprint-01-engineering-backlog.md)
