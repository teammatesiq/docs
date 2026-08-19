# TeamMates documentation agent instructions

These instructions apply to every automated or human-assisted change in this repository.

## Read first

Before proposing a material change, read:

1. `docs/governance/delivery-operating-model.md`
2. `docs/governance/sme-v1-current-release-boundary.md`
3. `docs/governance/cross-repository-baseline-manifest.md`
4. `docs/README.md`
5. the specifications directly affected by the change

Do not rely on chat memory as the sole source of authority.

## Non-negotiable SME v1 decisions

- Admin TeamMate is the only SME v1 TeamMate.
- Project TeamMate and all other TeamMate roles are outside SME v1.
- The deployed lifecycle is Configuring → Probation → Active → Suspended → Archived.
- A deployed TeamMate has no Draft state.
- Customer-facing Paused maps to `status = suspended` with `suspension_reason = customer_paused`.
- TeamMates platform identity and connected Microsoft identity are separate boundaries.
- A connected Microsoft identity never grants TeamMates organisation membership.
- Current Microsoft permissions are delegated `Mail.Read` and `Calendars.Read` only.
- No Microsoft write permission, file authority or consequential external action is enabled.
- Production launch requires an explicit Founder decision.

## Current versus target state

Some Draft specifications describe intended future capability. Never rewrite future capability as currently available or authorised.

When a current release fact conflicts with broader Draft wording, the controlled release-boundary record and baseline manifest govern the current candidate.

Do not introduce or imply:

- `Mail.Send`, `Mail.ReadWrite` or `Calendars.ReadWrite`;
- Microsoft Graph application permissions;
- file access or sharing;
- recipient or attendee contact;
- autonomous external action;
- another TeamMate role;

unless a controlling GitHub issue contains the required Founder decision and the baseline is updated.

## Change workflow

For a material change:

1. Identify the controlling GitHub issue or recorded Founder decision.
2. State whether the change affects current release scope, target-state intent, or both.
3. Update every materially affected canonical document.
4. Update `docs/README.md` when document version, status or classification changes.
5. Update the baseline manifest and release boundary when a controlled revision, permission, workflow or release gate changes.
6. Use a focused branch and pull request.
7. Explain scope, non-goals, authority, risk and validation.
8. Stop and escalate to Orchestration when authoritative sources conflict.

## Documentation standards

- Use precise customer, product, architecture and security terminology.
- Distinguish implemented, controlled-beta, prototype, planned and prohibited capability.
- Give material documents title, version, status, owner and updated date.
- Preserve exact issue numbers, revisions, schema versions and workflow-run IDs where they are part of release evidence.
- Use relative Markdown links for files within this repository.
- Avoid duplicating executable application detail that is better governed in `teammatesiq/platform`; link to the exact implementation evidence instead.
- Do not describe a prototype as production behaviour.
- Do not state that an external action occurred when the controlled release performs only an internal review action.

## Security and privacy

Never commit:

- passwords, API keys, access tokens or private keys;
- customer email, calendar, document or draft content;
- personal data or production datasets;
- live tenant/object identifiers unless they are already intentionally recorded as controlled operational evidence and their inclusion is necessary and approved.

Use content-free operational descriptions and metadata-only evidence.

## Review routing

- Product scope or workflow: Product Authority.
- Architecture, data, integration or reliability: Technical Design Authority.
- UX, content, accessibility or brand: Experience Authority.
- Security, privacy, permission or legal: Trust Authority.
- AI grounding, uncertainty or escalation: AI Behaviour Authority.
- Test evidence or release status: QA & Release Assurance.
- Cross-domain conflict or Founder gate: Founder & Orchestration.

Specialist recommendations do not become implementation authority until reconciled and recorded.