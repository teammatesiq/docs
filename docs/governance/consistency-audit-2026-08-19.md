---
Document title: TeamMates Cross-Repository Consistency Audit
Version: 1.0
Status: Controlled audit record
Owner: Orchestration
Audit date: 2026-08-19
---

# 1. Objective

Assess whether TeamMates strategy, canonical documentation, Lovable reference experience, production implementation, GitHub delivery controls and specialist-chat operating model describe one coherent SME v1 product.

# 2. Scope reviewed

- `teammatesiq/docs` at starting revision `45849f7ca1c181ad6c3f446e46605e0a3d5949d6`;
- `teammatesiq/platform` corrected release candidate `48ad426950d8ce37ac8f336c89bff4d0d9b4424c` and observed `main` revision `cdec17e4f17bfbeb7c37f96486e4baf4cdc7ac59`;
- `teammatesiq/teammate-colleague-hub` at `a2c92b8df6caca18673e5ad634a35ecdfbaedd8c`;
- launch-control issues #106, #109, #88, #149 and #154;
- current role-chat design and implementation handoff method.

# 3. Overall conclusion

The product direction is coherent and the software implementation has materially advanced beyond the original documentation baseline. The principal risk is no longer missing product definition; it is authority drift between stale documents, active GitHub issues, chat instructions, prototype behaviour and production code.

The remediation in this change establishes:

- one authority model;
- one mandatory delivery route;
- a current release-boundary record;
- a cross-repository baseline manifest;
- substantive replacements for six placeholder specifications;
- repository-level agent instructions;
- corrected release-gate records.

# 4. Findings and remediation

## F-001 — Canonical register materially understated repository maturity

**Severity:** High  
**State before remediation:** Open

The register stated that six specifications were placeholders, no audit or manifest existed, and engineering artefacts had not been created. In parallel, the production repository had reached schema v26, a deployed release candidate, six customer-facing acceptance journeys and extensive automated assurance.

**Remediation:**

- replace all six placeholder specifications with substantive controlled documents;
- update the canonical register;
- create this audit and the cross-repository baseline manifest;
- distinguish documentation artefacts from executable artefacts held in `teammatesiq/platform`.

**Post-change state:** Resolved by this pull request.

## F-002 — Target-state specifications could be mistaken for current permission authority

**Severity:** Critical if misinterpreted  
**State before remediation:** Open

Several Draft specifications describe future approval-controlled email sending, calendar mutation, file access, contacts and knowledge retrieval. The current release candidate authorises delegated `Mail.Read` and `Calendars.Read` only and enables no consequential external action.

**Remediation:**

- create the controlled SME v1 Current Release Boundary;
- state that broader Draft wording is target-state intent, not activation authority;
- encode the same ceiling in repository `AGENTS.md` files;
- require an explicit Founder gate for permission or external-effect expansion.

**Post-change state:** Resolved as a governance ambiguity; future capability remains unimplemented and unapproved.

## F-003 — Obsolete documentation pull request remained open

**Severity:** High  
**State before remediation:** Open

Docs pull request #2 was based on the pre-implementation state and included proposed integration contracts that no longer represented the controlled release boundary.

**Remediation:**

- add a supersession notice;
- rename and close PR #2 without merge;
- record the supersession in the baseline manifest.

**Post-change state:** Resolved on 19 August 2026.

## F-004 — Release issue recorded a resolved Azure blocker as current

**Severity:** Medium  
**State before remediation:** Open

Issue #109 and child issue #149 still presented Microsoft Key Vault provider registration as the current release blocker after exact calendar recovery run `32243424349` had succeeded.

**Remediation:**

- close #149 as completed with exact evidence;
- rewrite #109 around the actual remaining internal-alpha acceptance, monitoring, rollback and residual-risk gates.

**Post-change state:** Resolved on 19 August 2026.

## F-005 — Too many specialist chats could act as peer authorities

**Severity:** High  
**State before remediation:** Open

The role design included Product, Software, UX, Security, AI Behaviour, Commercial, QA, Platform, Data, Legal, Customer Success and Brand chats without a sufficiently explicit authority hierarchy. This created a risk of contradictory direct prompts to execution tools.

**Remediation:**

- establish eight authorities in the Delivery Operating Model;
- place Data & Integrations and Platform/DevOps/Reliability under Technical Design Authority;
- place Legal/Privacy under Trust Authority;
- place Customer Implementation & Success under Commercial Authority before launch;
- keep AI Behaviour separate from independent QA;
- reserve programme reconciliation to Founder & Orchestration.

**Post-change state:** Governance resolved; ChatGPT Project chat renaming/archiving requires a manual project-interface action.

## F-006 — Chat history was being used as an implicit implementation bridge

**Severity:** High  
**State before remediation:** Open

ChatGPT Project memory and Codex history are useful context but do not constitute one guaranteed shared state. An instruction such as “build what the other chats agreed” is not deterministic.

**Remediation:**

- require one controlling GitHub issue and implementation brief;
- define exact information required in a Codex handoff;
- add repository `AGENTS.md` instructions;
- make GitHub, not chat memory, the durable decision and evidence record.

**Post-change state:** Resolved by operating model and repository controls.

## F-007 — Production repository lacked root agent instructions

**Severity:** High  
**State before remediation:** Open

No root `AGENTS.md` was present in `teammatesiq/platform`, so a fresh coding thread could begin without the non-negotiable product, lifecycle, permission and validation boundaries.

**Remediation:**

- add root `AGENTS.md`;
- add narrower instructions for `apps/web`, `apps/api` and `apps/worker`;
- add an implementation-handoff template;
- add prototype-specific agent instructions to the Lovable repository.

**Post-change state:** Addressed by linked platform and prototype pull requests.

## F-008 — Lovable authority required durable enforcement

**Severity:** Medium  
**State before remediation:** Partially controlled

The prototype README correctly stated that Lovable must not invent authoritative backend logic. That boundary depended mainly on a long initial project brief.

**Remediation:**

- retain the README boundary;
- add a root `AGENTS.md` to make the rule durable for future Lovable and coding sessions;
- state that the production TMOS backend and canonical docs remain authoritative.

**Post-change state:** Addressed by linked prototype pull request.

## F-009 — Current launch work and next-slice work needed explicit separation

**Severity:** High  
**State before remediation:** Partially controlled

Issue #154 authorises a valuable Trusted Draft Workbench next slice while #109 still controls internal-alpha acceptance of the pinned release candidate. Without a durable boundary, parallel implementation could accidentally replace or broaden the candidate.

**Remediation:**

- record #154 as default-off and outside the pinned candidate;
- prohibit it from adding Microsoft write permissions or external effects;
- require separate acceptance before private beta;
- encode the distinction in the release plan, release-boundary document and platform agent instructions.

**Post-change state:** Resolved as a governance boundary; implementation and evidence remain open.

## F-010 — Main branches are not protected through GitHub settings

**Severity:** High  
**State before remediation:** Open

At audit time, GitHub reported `main` as unprotected for the docs, platform and prototype repositories. Repository files can add CODEOWNERS and workflows, but they cannot by themselves enforce required reviews, status checks, force-push restrictions or branch-deletion restrictions.

**Remediation:**

- add or strengthen CODEOWNERS where appropriate;
- retain issue `teammatesiq/platform#1` as the enforcement work item;
- require the repository owner to enable branch protection/rulesets in GitHub settings and capture evidence.

**Post-change state:** Open manual repository-administration action. It is not a production capability blocker but is a material governance control.

## F-011 — An obsolete workplace-insights concept could contaminate project memory

**Severity:** Medium  
**State before remediation:** Open

An earlier TeamMates/Lovable direction described workplace analytics, collaboration patterns, meeting load and employee-detail views. It conflicts with the approved governed-digital-colleague proposition.

**Remediation:**

- define the canonical chat register;
- require the obsolete chat to be renamed `OBSOLETE — DO NOT USE` or removed from the TeamMates Project;
- prohibit workplace-insights scope from entering implementation without a new Founder decision.

**Post-change state:** Manual ChatGPT Project action remains.

# 5. Remaining open actions

| Action | Owner | Gate |
|---|---|---|
| Complete live signed-in internal-alpha acceptance under #109 | QA-Release with Founder test principal | Release gate |
| Complete Important Email review-only acceptance under #88 | Founder / QA-Release | Release gate |
| Record monitoring, rollback, recovery and residual-risk evidence | QA-Release and Platform/Reliability | Release gate |
| Enable and evidence GitHub branch protection/rulesets | Repository owner | Governance control |
| Rename active chats to the canonical authority register | Founder | Operating-model control |
| Rename/remove the obsolete workplace-insights chat | Founder | Project-memory control |
| Complete and independently assure #154 behind default-off controls | Product, Engineering, Trust and QA | Next-slice gate |
| Give explicit Founder approval before production launch | Founder | Production gate |

# 6. Baseline readiness conclusion

After the repository pull requests linked to this audit are merged, TeamMates has a usable controlled cross-repository baseline for continued internal-alpha and bounded next-slice development.

This conclusion does not mean:

- production is approved;
- future Microsoft permissions are approved;
- external actions are enabled;
- all target-state requirements are implemented;
- open release evidence may be skipped.

The remaining work is clearly gated rather than structurally undefined.