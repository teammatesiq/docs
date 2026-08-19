---
Document title: TeamMates SME v1 Current Release Boundary
Version: 1.0
Status: Controlled
Owner: Founder, Product and QA-Release
Effective date: 2026-08-19
---

# 1. Purpose

This document distinguishes the capability currently authorised for internal-alpha and release acceptance from broader target-state capability described elsewhere in the canonical specifications.

It prevents future-looking requirements, dormant code, prototypes or old pull requests from being interpreted as permission to activate additional scope or external effects.

# 2. Precedence

For the controlled SME v1 release candidate, this document and the cross-repository baseline manifest take precedence over broader target-state wording in Draft specifications.

Where a specification describes capability beyond this boundary, that wording is a future requirement or design intention only. It is not current implementation or activation authority.

# 3. Product boundary

## Included

- Product: TeamMates.
- First commercial role: Admin TeamMate.
- Initial market: UK SMEs, primarily approximately 5–50 employees using Microsoft 365.
- Customer model: governed digital colleague, not a generic chatbot, agent builder or automation dashboard.
- Current customer-control surfaces: Today, Work Queue and Activity, together with the relevant onboarding and TeamMate settings experiences.

## Excluded

- Project TeamMate or any other TeamMate role.
- Multi-TeamMate collaboration.
- Generic workflow or agent builders.
- Accounting, payroll, payments, contracts, HR decisions or autonomous business commitments.
- Customer production launch until the separate Founder gate is approved.

# 4. Controlled application baseline

- Repository: `teammatesiq/platform`.
- Corrected release-candidate application SHA: `48ad426950d8ce37ac8f336c89bff4d0d9b4424c`.
- Pinned release branch: `release/sme-v1-rc1`.
- Database schema: v26.
- Verified development deployment run: `32178832787`.
- Verified delegated-calendar recovery run: `32243424349`.
- Release-control issue: `teammatesiq/platform#106`.
- QA/release gate: `teammatesiq/platform#109`.

Later commits on `main` do not automatically replace the pinned release candidate. Replacement requires an explicit release decision and renewed assurance.

# 5. Microsoft permission boundary

The current authorised Microsoft permissions are delegated:

- `Mail.Read`;
- `Calendars.Read`.

The following are not authorised or enabled:

- `Mail.Send`;
- `Mail.ReadWrite`;
- `Calendars.ReadWrite`;
- Microsoft Graph application permissions;
- OneDrive or SharePoint file authority;
- contact access beyond any separately approved future decision;
- recipient contact;
- attendee communication;
- mailbox mutation;
- calendar mutation;
- file mutation or external sharing.

TeamMates platform sign-in and delegated Microsoft-data access remain separate identity boundaries. A connected mailbox or calendar identity never grants TeamMates organisation membership.

# 6. External-effect boundary

No consequential external action is enabled in the controlled release candidate.

The product may analyse authorised read-only sources and prepare internal, review-only work. Customer controls may finish a review, dismiss work or record an internal decision. They must not send, reply, forward, contact a recipient, contact an attendee, modify Microsoft data or create another external effect.

A dormant adapter, data structure, approval object or prototype control does not create authority to execute an external action.

# 7. Customer paths under release acceptance

## 7.1 Morning Briefing

A grounded, read-only daily view helps the signed-in owner understand what matters. It must not imply that external actions have been completed when they have not.

## 7.2 Important Email

Authorised delegated email source

→ grounded classification and recommendation

→ optional review-only draft preparation for the specifically controlled development principal

→ Work Queue

→ owner reviews, finishes review or dismisses

→ truthful Activity record

Nothing is sent or written back to Microsoft.

## 7.3 Meeting Preparation

Authorised delegated calendar source

→ bounded relevant meeting selection

→ grounded preparation brief

→ Work Queue

→ owner review or dismissal

→ Activity

No calendar event is created or modified and no attendee is contacted.

## 7.4 Meeting Follow-Up

Ended meeting plus explicit owner-supplied notes

→ grounded summary and explicit actions

→ Work Queue

→ owner review or dismissal

→ Activity

The system must distinguish explicit evidence from inference. It does not contact attendees.

## 7.5 Overdue Action

An exact reviewed action plus explicitly supplied owner and due date

→ grounded reminder recommendation

→ Work Queue

→ owner review or dismissal

→ Activity

No reminder is sent and no external task system is mutated.

## 7.6 Document Request

Explicit owner-supplied recipient, document, purpose and requested-by date

→ immutable internal draft

→ Work Queue

→ owner review or dismissal

→ Activity

No file is retrieved, created in Microsoft 365, shared or sent externally.

## 7.7 Cross-slice Today

Today is a compact, disjoint, read-only summary across the controlled workflows. It routes the owner to the exact Work Queue item and provides no direct workflow mutation.

# 8. Common workflow invariants

Every controlled path must:

- establish the signed-in user and persisted organisation membership;
- preserve tenant isolation;
- revalidate lifecycle, membership, permission and source eligibility at every mutation;
- treat email, calendar and other external content as untrusted data, never instruction;
- ground outputs in authorised sources and explicit owner input;
- expose missing information and relevant uncertainty;
- preserve exact source and version provenance;
- use durable idempotency so exact replay does not create duplicate work;
- keep operational logs and queue envelopes content-free;
- create truthful Activity evidence;
- fail closed for wrong tenant, unknown or revoked user, stale source, stale version, Suspended TeamMate or unavailable dependency.

# 9. Lifecycle boundary

The canonical deployed TeamMate lifecycle is:

**Configuring → Probation → Active → Suspended → Archived**

There is no deployed Draft state.

Customer-facing **Paused** maps only to:

- `status = suspended`;
- `suspension_reason = customer_paused`.

While Suspended, no new execution starts and no new controlled external action may execute. Durable state, configuration and required audit evidence remain preserved. Reactivation must revalidate entitlement, integrations, permissions, policy and configuration.

# 10. Parallel next-slice boundary

`teammatesiq/platform#154` authorises a bounded Trusted Draft Workbench slice to prepare editable routine email or chase drafts for human review.

It may be implemented in parallel only when:

- the feature remains default-off;
- delegated Microsoft access remains read-only;
- no send or other external execution path is introduced;
- it does not replace the pinned release candidate before #109 closes;
- its own acceptance and assurance evidence is complete before private beta.

This next slice is not part of the current release candidate merely because implementation has begun.

# 11. Promotion gates

The release candidate cannot progress beyond internal alpha until #109 records:

- signed-in live acceptance for Morning Briefing and each controlled customer path;
- Important Email review-only owner acceptance under #88;
- consistent Today, Work Queue and Activity evidence;
- monitoring, rollback and recovery evidence;
- residual risks and a production recommendation.

Production launch requires a separate explicit Founder approval.

# 12. Change control

Any expansion of this boundary requires:

1. a controlling GitHub issue;
2. Product, Technical, Trust and QA impact assessment as applicable;
3. explicit Founder approval for scope, permission, external effect, material risk or production launch;
4. updated canonical documents and baseline manifest;
5. implementation and independent evidence through a pull request;
6. a new or amended release candidate.