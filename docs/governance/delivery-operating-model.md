---
Document title: TeamMates Delivery Operating Model
Version: 1.0
Status: Controlled
Owner: Founder and Orchestration
Effective date: 2026-08-19
---

# 1. Purpose

This document defines how TeamMates product decisions, specialist advice, prototypes, software changes and release evidence move from idea to production.

It exists to prevent:

- multiple specialist chats behaving as equal product authorities;
- contradictory instructions reaching Lovable or Codex;
- chat history being treated as a durable decision record;
- prototypes inventing authoritative backend behaviour;
- implementation expanding permissions, scope or external effects without approval;
- delivery effort drifting away from customer-visible outcomes.

# 2. Governing principle

The operating chain is:

**Founder sets direction → Orchestration controls the programme → specialist authorities shape and review → GitHub records the approved position → Lovable prototypes experience where useful → Codex implements bounded changes → QA independently gates release.**

No specialist chat, prototype or coding agent may bypass this chain for a material change.

# 3. Authority model

## 3.1 Founder and Orchestration

**Accountable authority:** Matt as Founder, supported by the Orchestration chat.

Owns:

- product and company direction;
- prioritisation and sequencing;
- resolution of cross-domain conflicts;
- founder decisions and risk acceptance;
- the approved implementation brief;
- deciding what is handed to Lovable or Codex;
- production-launch approval.

Orchestration is not another specialist opinion. It reconciles specialist input and maintains one programme position.

## 3.2 Product Authority

**Primary chat:** Product / Admin TeamMate.

Owns:

- customer problem and outcome;
- SME v1 scope and non-goals;
- workflow intent;
- product acceptance criteria;
- value hypotheses and product measures;
- product-language decisions not reserved to Brand.

Product does not approve security exceptions, architecture expansion or production release.

## 3.3 Technical Design Authority

**Primary chat:** Head of Software.

Owns:

- software architecture and component boundaries;
- technical decomposition;
- engineering standards;
- build-versus-buy recommendations;
- technical review of implementation changes;
- consolidation of Data & Integrations and Platform/DevOps/Reliability advice.

Data & Integrations and Platform/DevOps/Reliability operate as specialist disciplines under this authority rather than as parallel product authorities.

## 3.4 Experience Authority

**Primary chats:** UX & CX, supported by Head of Brand.

Owns:

- customer journeys and information architecture;
- interaction design and human-control experience;
- accessibility and responsive behaviour;
- customer-facing language and design-system application;
- consolidated Lovable briefs.

Head of Brand governs brand, terminology, claims and visual consistency. It does not independently expand product capability.

## 3.5 Trust Authority

**Primary chat:** Security & Governance, supported by Legal, Privacy & Compliance.

Owns:

- security controls and threat boundaries;
- privacy and data-minimisation requirements;
- permission ceilings and external-effect controls;
- tenant isolation and access-control review;
- legal and compliance review;
- residual-risk recommendation.

Trust may block unsafe delivery. Material residual-risk acceptance remains a Founder decision.

## 3.6 AI Behaviour Authority

**Primary chat:** AI Behaviour Lead.

Owns:

- grounding and evidence rules;
- uncertainty and escalation behaviour;
- prompt-injection and untrusted-content handling;
- behavioural policy and prohibited output;
- model-independent evaluation cases;
- the definition of acceptable AI behaviour.

AI Behaviour does not independently certify its own implementation.

## 3.7 Independent Assurance

**Primary chat:** QA & Evaluation / QA-Release.

Owns:

- test strategy and release evidence;
- regression and live acceptance;
- independent evaluation of product and AI behaviour;
- verification of security-critical invariants;
- release recommendation and go/no-go evidence.

QA remains separate from AI Behaviour and implementation so that the party defining or building behaviour is not the sole party judging it.

## 3.8 Commercial Authority

**Primary chats:** Commercial Lead and Customer Implementation & Success.

Owns:

- ideal customer profile and qualification;
- packaging, pricing hypotheses and sales motion;
- pilot recruitment and onboarding;
- adoption, retention and customer-success measures;
- evidence-backed commercial claims.

Before launch, Customer Implementation & Success operates within the Commercial authority rather than as a separate programme authority.

## 3.9 Execution tools

### Lovable

Lovable is a customer-experience prototype and reference-frontend tool. It may explore journeys, layouts, language and interaction patterns. It must not define authoritative permissions, policy, tenant isolation, lifecycle, workflow orchestration, audit, Microsoft Graph execution, AI execution or knowledge security.

### Codex

Codex implements bounded GitHub issues in the production repositories. It may inspect, edit, test and propose pull requests within the authority supplied by the issue and repository instructions. It may not make product, permission, external-effect or production-launch decisions.

### GPT-5.3-Codex-Spark

Spark is appropriate for small, targeted, interactive changes after scope and design are settled. Cross-cutting architecture, migrations, security-critical changes and ambiguous multi-service work require a stronger coding model and explicit specialist review.

# 4. Source-of-truth order

For material work, use the following order:

1. An explicit Founder decision recorded in GitHub.
2. The current cross-repository baseline manifest and release-boundary record.
3. Canonical product, architecture, security, UX and test specifications in `teammatesiq/docs`.
4. Accepted issues, pull requests, code, migrations and tests in `teammatesiq/platform` for implemented behaviour.
5. The Lovable reference implementation in `teammatesiq/teammate-colleague-hub` for experience intent only.
6. Chat history and model memory as working context, never as the sole durable authority.

When two higher-order sources conflict, stop and route the conflict to Orchestration. Do not silently choose one or create a hybrid interpretation.

# 5. Mandatory delivery flow

Every material change follows this route.

## 5.1 Outcome definition

Product or Orchestration defines:

- the customer or operational outcome;
- why it matters now;
- scope and explicit non-goals;
- success and acceptance criteria;
- whether a Founder decision is required.

## 5.2 GitHub issue

Before implementation, one controlling GitHub issue records:

- owner and delivery stream;
- current baseline and dependencies;
- canonical references;
- permission and external-effect ceiling;
- required tests and live evidence;
- required specialist reviewers;
- stop conditions and Founder gates.

## 5.3 Specialist shaping

Only the authorities materially affected by the change shape or review it. Orchestration resolves conflicts and produces one approved implementation brief.

Specialist chats must not issue competing implementation prompts directly to Codex or Lovable.

## 5.4 Experience prototyping

Lovable is used only where customer interaction would benefit from visual exploration. The brief must state which elements are reference experience and which existing TMOS APIs or policies remain authoritative.

## 5.5 Implementation

One primary Codex thread owns each bounded implementation issue. It must:

- read repository `AGENTS.md` instructions first;
- inspect surrounding code and current tests;
- preserve current architecture and permission boundaries;
- use a dedicated branch and pull request;
- implement the smallest complete customer or operational outcome;
- run the required validation;
- report anything not verified.

Read-heavy subagents may be used for codebase exploration, security review, test-gap analysis, maintainability review and documentation consistency. Multiple agents must not make overlapping writes to the same code area without an explicit partition and integration owner.

## 5.6 Independent review and release

QA and required specialist authorities review the pull request and evidence. Merge does not itself authorise feature activation or production launch.

Feature activation, external permissions, consequential actions and production release remain separately gated.

## 5.7 Documentation and programme closure

The implementation pull request, or a linked documentation pull request merged with it, updates:

- changed canonical behaviour;
- current release-boundary records;
- migrations and API contracts where applicable;
- test/evaluation coverage;
- the controlling issue and programme status.

# 6. Founder decision gates

Explicit Founder approval is required before any change that:

- alters the product proposition or SME v1 scope;
- introduces another TeamMate into SME v1;
- changes the canonical TeamMate lifecycle;
- expands Microsoft or other provider permissions;
- enables a consequential external action;
- creates material new cost or operational exposure;
- accepts material residual security, legal, privacy or reliability risk;
- changes a canonical architecture decision;
- promotes a release to production.

No approval is implied by possession of code, a dormant adapter, a prototype control or a passing unit test.

# 7. Current programme phase

As at 19 August 2026:

- Issue `teammatesiq/platform#106` controls the SME v1 launch critical path.
- Issue `teammatesiq/platform#109` owns internal-alpha acceptance and release assurance.
- The corrected release candidate is pinned at application SHA `48ad426950d8ce37ac8f336c89bff4d0d9b4424c`, schema v26.
- Delegated Microsoft permissions remain `Mail.Read` and `Calendars.Read` only.
- No Microsoft write permission or consequential external action is enabled.
- Issue `teammatesiq/platform#154` may proceed in parallel as a default-off product slice but must not replace or broaden the pinned release candidate before the release gate closes.
- No new horizontal platform foundation, generic workflow framework or dormant external-action work enters the launch path without a proven P0 defect or explicit Founder decision.

# 8. Canonical chat register

The TeamMates ChatGPT Project should use the following active authority names:

| Order | Canonical chat | Authority |
|---:|---|---|
| 00 | Founder & Orchestration | Programme control and final reconciliation |
| 10 | Product Authority — Admin TeamMate | Customer outcome and scope |
| 20 | Technical Design Authority | Architecture and engineering |
| 30 | Experience Authority | UX, CX and brand consolidation |
| 40 | Trust Authority | Security, privacy, legal and governance |
| 50 | AI Behaviour Authority | Grounding, escalation and behavioural policy |
| 60 | QA & Release Assurance | Independent evidence and release gate |
| 70 | Commercial & Customer Success | Sales, pilots, onboarding and adoption |

The following remain supporting specialist chats, not peer programme authorities:

- Data & Integrations;
- Platform, DevOps & Reliability;
- Legal, Privacy & Compliance;
- Head of Brand.

Any earlier TeamMates chat based on workplace analytics, collaboration scoring, meeting-load analysis or employee-insight dashboards is outside the approved governed-digital-colleague proposition. It must be renamed `OBSOLETE — DO NOT USE` or removed from the TeamMates Project.

# 9. Working rules for chats

Each active authority chat should:

- use GitHub links and exact issue numbers when discussing live work;
- distinguish approved decisions from recommendations;
- record material decisions in GitHub before implementation;
- hand conflicts to Orchestration rather than negotiating indefinitely across chats;
- avoid restating the whole programme in every prompt;
- avoid instructing Codex or Lovable directly unless acting from an Orchestration-approved issue.

# 10. Review of this operating model

This model is reviewed when:

- the company adds permanent human team members;
- a second TeamMate enters active product scope;
- the delivery repository structure changes;
- a material governance failure occurs;
- the Founder changes the decision model.

Changes require a Founder decision recorded through a pull request.