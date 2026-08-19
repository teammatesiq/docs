---
Document title: Admin TeamMate UX/UI Specification
Version: 1.1
Status: Controlled
Owner: Experience Authority
Last updated: 2026-08-19
---

# 1. Purpose

This document defines the customer experience, information architecture, interaction states, content rules, accessibility expectations and reference-prototype boundary for Admin TeamMate.

The experience must make governed work feel simple without hiding important evidence, limitations or human-control requirements.

# 2. Experience proposition

TeamMates should feel like the customer has hired a capable digital colleague, not opened an AI control panel.

The experience should repeatedly answer:

> This is what I have taken care of.

> This is what I need from you.

> This is what matters next.

The interface must help the customer delegate and review work rather than operate model settings or construct automation logic.

# 3. Experience principles

## 3.1 Colleague, not chatbot

Admin TeamMate has a role, responsibilities, access and current status. Present it as a professional colleague profile rather than a bot avatar or generic chat window.

Chat may be an interaction surface, but important work must also exist in durable product surfaces.

## 3.2 Outcome before technology

Lead with the work prepared, its relevance and the required customer action. Do not lead with model names, tokens, prompts, agents or technical execution steps.

## 3.3 Human control without administrative burden

The user should be able to review routine work quickly while still understanding:

- source;
- evidence;
- material assumptions;
- missing information;
- the exact effect of their action.

## 3.4 Truthful effect language

The UI must describe what actually happened.

Examples:

- use **Draft for review only**, not **Email ready to send**, when no sending exists;
- use **Finish draft review**, not **Approve and send**, when the action is internal;
- use **Reminder recommendation reviewed**, not **Reminder sent**;
- use **Internal document draft**, not **Document shared**.

## 3.5 Calm clarity

Use generous whitespace, strong typography and clear hierarchy. Avoid dense enterprise dashboards, excessive alerts, neon AI styling, robots, gimmicky motion and unexplained technical states.

## 3.6 Evidence in context

Evidence should be visible where the customer makes a decision, not hidden in a separate audit tool.

## 3.7 Safe incompleteness

It is better to show Needs Your Input or a partial grounded result than to fabricate completeness.

## 3.8 Mobile-capable review

Core review, dismissal, input and pause actions must work on mobile web even where configuration is primarily desktop-oriented.

# 4. Primary users

## 4.1 Organisation Owner

Needs to:

- create/select the organisation;
- hire/configure Admin TeamMate;
- connect Microsoft sources;
- understand permissions and limitations;
- review work and lifecycle status;
- pause, reconnect or seek support;
- view trust/governance and billing where available.

## 4.2 Member or delegated user

May need to:

- view authorised Today and Work Queue items;
- supply explicit input;
- review work within their role;
- understand why access is unavailable.

Membership and permission enforcement remain server-owned. The UI must not infer access from a connected Microsoft account.

## 4.3 Internal-alpha tester

Needs clear environment, feature and no-external-effect cues so live acceptance cannot be confused with production or send authority.

# 5. Information architecture

## 5.1 Current controlled surfaces

The production experience should prioritise:

### Today

Compact read-only view of what matters now. It summarises disjoint workflow items and routes to the exact Work Queue item.

### Work Queue / Work

Primary human-control surface for prepared work, active work, missing input and recently completed outcomes.

### Activity

Truthful, traceable history of meaningful internal outcomes and lifecycle changes.

### Admin TeamMate profile

Role, status, current access, connection health, responsibilities and lifecycle controls.

### Settings

Organisation, connection, preference and support settings within the customer’s authority.

### Trust & Governance

For authorised organisation administrators: access, permission, evidence, lifecycle and relevant policy information.

## 5.2 Reference-prototype surfaces

The Lovable reference may also explore:

- TeamMates;
- Ask Alex;
- Knowledge;
- Billing;
- broader colleague profile and onboarding journeys.

A prototype surface does not become production scope merely because it exists visually. Production inclusion requires a controlling issue, current API behaviour and acceptance evidence.

## 5.3 Desktop navigation

Where the full reference information architecture is used, preferred labels are:

- TeamMates;
- Today;
- Work;
- Ask Alex;
- Knowledge;
- Alex;
- Settings;
- Trust & Governance for organisation administrators;
- Billing for authorised administrators.

## 5.4 Mobile navigation

Prioritise:

- Today;
- Work;
- Ask;
- Alex.

Do not bury urgent review or Needs Your Input work behind configuration-oriented navigation.

# 6. Onboarding experience

## 6.1 Welcome

Recommended headline:

**Meet your new Admin TeamMate.**

Explain in customer language that Admin TeamMate helps keep on top of email, meetings, actions and routine admin.

Primary action:

**Hire Admin TeamMate**

## 6.2 Meet the TeamMate

Present:

- name, such as Alex in the demonstration experience;
- role: Admin TeamMate;
- concise role description;
- responsibilities;
- current lifecycle status;
- what the role will not do.

## 6.3 Permission explanation

Before connection, show:

- what data is requested;
- why it is needed;
- what TeamMates can do with it;
- what TeamMates cannot do;
- that current permissions are delegated `Mail.Read` and `Calendars.Read` only;
- that no email, calendar or file is changed;
- how access can be disconnected.

Do not hide scope behind generic wording such as “connect Microsoft 365.”

## 6.4 Connection states

Support:

- not connected;
- connecting;
- connected and healthy;
- connected but permission incomplete;
- expired/revoked;
- unavailable dependency;
- wrong or unsupported identity;
- reconnect required.

Each state should offer the next safe action without exposing secrets or another tenant.

## 6.5 Probation introduction

Explain that Probation:

- validates access and useful work;
- keeps work reviewable;
- surfaces uncertainty clearly;
- does not grant additional permission automatically;
- may complete based on readiness rather than elapsed time alone.

# 7. Today

## 7.1 Purpose

Today answers:

- what matters now;
- what is prepared;
- what needs input;
- where to go next.

## 7.2 Content model

Each item should include only the minimum needed to orient the user:

- workflow or work type;
- concise outcome/title;
- timing or urgency where grounded;
- current state;
- source cue;
- exact navigation target.

## 7.3 Rules

- Today is read-only in the controlled release.
- Do not duplicate one logical item across sections.
- Do not put review mutations directly on Today.
- Preserve exact navigation to Work Queue.
- Empty states should state whether there is no work or whether a dependency is unavailable.
- Do not imply completeness when only some sources are connected.

# 8. Work Queue

## 8.1 Purpose

Work Queue is where the customer understands and controls meaningful work.

## 8.2 Primary states

### Ready For You

Prepared work awaits review or a customer decision.

### Working

Work is actively being prepared or a permitted internal step is in progress.

### Needs Your Input

The TeamMate cannot continue safely without specific information or judgement.

### Completed

A recent truthful terminal outcome is available.

## 8.3 Work item anatomy

A material work item should show:

- title and workflow type;
- current state;
- why it matters;
- source and source timing;
- prepared output;
- evidence used;
- material assumptions;
- missing information;
- actual available action;
- what that action will and will not do;
- version/staleness feedback where relevant.

## 8.4 Review controls

Use controls that match the internal effect, such as:

- Review;
- Finish review;
- Edit draft;
- Reject;
- Dismiss;
- Provide information;
- View source;
- Try again where safe.

Do not expose Send, Reply, Forward, Share, Create meeting or Contact attendee under the current release boundary.

## 8.5 Optimistic concurrency

When a work item is stale:

- preserve the customer’s unsaved text where safe;
- state that a newer version exists;
- prevent an incorrect mutation;
- allow refresh/review of the current version;
- do not present a generic success state.

# 9. Workflow-specific experience

## 9.1 Morning Briefing

Present a concise view, not a long report. Prioritise:

- important work;
- upcoming preparation;
- Needs Your Input;
- prepared items.

Each entry links to the relevant source or Work Queue item.

## 9.2 Important Email

Show:

- why the email is considered important;
- source/thread cue;
- evidence and missing context;
- review-only draft label;
- explicit statement that nothing will be sent;
- Prepare draft only for the controlled eligible principal;
- Finish draft review and Dismiss draft actions.

Unapproved users must not see the control, and direct endpoint denial must not disclose the approved principal.

## 9.3 Meeting Preparation

Show:

- meeting title, time and confirmed attendee evidence;
- preparation brief;
- what source is and is not available;
- missing context;
- no implication that the calendar was updated or attendees contacted.

## 9.4 Meeting Follow-Up

Separate:

- meeting facts;
- owner-supplied notes;
- explicit decisions/actions;
- inferred or missing fields.

Do not style an inferred owner/date as confirmed.

## 9.5 Overdue Action

Show the exact action, explicit owner, due date, source meeting and why it is overdue. Label the output as a reminder recommendation, not a sent chase.

## 9.6 Document Request

Show the exact owner-supplied recipient, document, purpose and requested-by date. Label the output as an internal draft. Do not imply file retrieval, creation, sharing or delivery.

## 9.7 Trusted Draft Workbench

When #154 is implemented and enabled in an approved environment:

- provide an editable draft surface;
- keep source and evidence visible;
- preserve missing-information and escalation states;
- show generated/source version and stale-state handling where useful;
- route complaints, refunds, prices, quotes, negotiations and commitments to Needs Your Input;
- state clearly that finishing review does not send the message.

# 10. Activity

Activity should record meaningful events such as:

- work prepared;
- review finished;
- work dismissed or rejected;
- information requested or supplied;
- safe failure;
- lifecycle paused/reactivated;
- connection changed.

It must not:

- expose sensitive content unnecessarily;
- claim an external effect that did not occur;
- present infrastructure retries as multiple customer outcomes;
- reveal another tenant or user.

# 11. TeamMate profile and lifecycle

The profile should show:

- TeamMate name and role;
- current lifecycle status;
- concise responsibilities;
- connected sources and health;
- current access boundary;
- current enabled/available workflows at an appropriate level;
- last useful activity where appropriate;
- Pause/Resume or support actions within user authority.

## 11.1 Status language

Customer language may use **Paused**, but the system state remains Suspended with `customer_paused` reason.

Do not expose a deployed Draft state.

## 11.2 Pause confirmation

Explain:

- no new work will start;
- scheduled work will stop where appropriate;
- no external effect will occur;
- configuration and required history remain;
- resume will revalidate access and configuration.

# 12. Trust and governance experience

The customer should be able to understand:

- connected data sources;
- delegated permissions;
- what the TeamMate cannot do;
- human-review requirements;
- evidence and Activity;
- current lifecycle;
- how to disconnect access;
- how to report a concern.

Avoid presenting every internal control or architecture component. Translate controls into customer consequences.

# 13. Content and terminology

Prefer:

- TeamMate;
- prepared;
- review;
- source;
- evidence;
- needs your input;
- completed;
- responsibility;
- connection;
- pause;
- draft for review only.

Avoid unless in a technical/admin diagnostic context:

- LLM;
- RAG;
- embeddings;
- tokens;
- agent loop;
- context window;
- system prompt;
- vector database;
- autonomous agent.

Use sentence case for headings and controls unless brand standards require otherwise.

# 14. Interface states

Every critical surface must specify and test:

- loading;
- empty;
- partial data;
- success;
- Needs Your Input;
- permission denied;
- disconnected/revoked source;
- dependency unavailable;
- stale version;
- Suspended TeamMate;
- wrong/unknown organisation;
- safe retry;
- mobile layout.

Loading states must not falsely imply that work is being performed when the user lacks eligibility.

# 15. Error design

Customer errors should:

- state what could not be completed;
- distinguish temporary retry from required customer action;
- preserve work where safe;
- provide a correlation/support reference where appropriate;
- avoid source-content leakage in URLs, logs or generic diagnostics;
- avoid exposing internal Azure, queue, database or model details;
- never reveal another organisation’s existence.

# 16. Accessibility

Target WCAG 2.2 AA.

Minimum requirements:

- complete keyboard operation;
- visible focus;
- semantic headings, landmarks and controls;
- programmatic labels and error associations;
- sufficient contrast;
- no colour-only status communication;
- reduced-motion support;
- meaningful screen-reader announcements for asynchronous state changes;
- touch targets suitable for mobile;
- readable line length and scalable text;
- clear confirmation for destructive lifecycle or disconnect actions.

# 17. Responsive behaviour

## Desktop

Use available width for evidence and prepared work without turning the experience into a dense dashboard.

## Tablet

Preserve source, action and state hierarchy. Secondary evidence may collapse into clearly labelled disclosure.

## Mobile

Prioritise:

- current status;
- prepared output;
- what is needed;
- primary safe action;
- source/evidence access;
- pause/support access.

Do not require horizontal tables for critical customer actions.

# 18. Visual direction

The product should feel:

- intelligent;
- modern;
- confident;
- calm;
- trustworthy;
- professional;
- human.

Avoid:

- robot imagery;
- cartoon AI characters;
- science-fiction controls;
- neon AI gradients;
- generic chatbot chrome;
- excessive metric tiles;
- decorative motion that obscures state.

Use the approved TeamMatesIQ visual-identity and Flow Path assets from the brand governance set.

# 19. Lovable reference boundary

`teammatesiq/teammate-colleague-hub` is the customer-experience prototype/reference implementation.

Lovable may:

- explore journeys, content, layout and component behaviour;
- use realistic mocked data;
- maintain replaceable adapters/interfaces;
- demonstrate the colleague-like experience.

Lovable must not:

- invent authoritative permissions or policy;
- implement tenant isolation as UI-only logic;
- define lifecycle transitions independently;
- create production Microsoft Graph, AI, audit or knowledge-security logic;
- embed Supabase-specific business rules directly in components without explicit approval;
- present a prototype-only external effect as current product capability.

The production TMOS backend remains authoritative.

# 20. UX acceptance evidence

A material customer slice requires:

- component and interaction tests;
- signed-in browser acceptance;
- desktop and mobile coverage;
- success, empty, error, stale, Suspended and wrong-tenant paths where applicable;
- verification of truthful effect language;
- accessibility review for the critical path;
- Product, Experience and QA acceptance;
- Trust review where evidence, permissions or sensitive data presentation changes.

# 21. Related documents

- [Product Requirements](../strategy/product-requirements.md)
- [Admin TeamMate Role Handbook](../product/admin-teammate-role-handbook.md)
- [Admin TeamMate Workflows](../product/admin-teammate-workflows.md)
- [Admin TeamMate Onboarding and Probation](../product/admin-teammate-onboarding-probation.md)
- [TeamMate Interaction Model](../architecture/teammate-interaction-model.md)
- [SME v1 Current Release Boundary](../governance/sme-v1-current-release-boundary.md)
- [Tone, Terminology and Naming](../brand/tone-terminology-and-naming.md)
- [Visual Identity](../brand/visual-identity.md)
- [Test and Evaluation Specification](../engineering/test-evaluation-specification.md)