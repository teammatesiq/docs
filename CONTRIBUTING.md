# Contributing

Read [AGENTS.md](AGENTS.md), the [Delivery Operating Model](docs/governance/delivery-operating-model.md) and the [SME v1 Current Release Boundary](docs/governance/sme-v1-current-release-boundary.md) before changing a material TeamMates document.

## Making changes

1. Start from a controlling GitHub issue or recorded Founder decision.
2. Create a focused branch from `main`.
3. Identify whether the change affects current release scope, target-state intent, or both.
4. Update the relevant canonical documents and linked governance controls.
5. Update `docs/README.md` when a document version, status or classification changes.
6. Update the baseline manifest or release-boundary record when an exact revision, permission, workflow or gate changes.
7. Use clear commit messages.
8. Open a pull request explaining outcome, authority, scope, non-goals, risk and validation.
9. Obtain the required authority reviews before merging.

## Pull request requirements

A substantive pull request should state:

- controlling issue or Founder decision;
- documents and product behaviour affected;
- current versus target-state impact;
- Microsoft permission and external-effect impact;
- lifecycle, identity, tenancy, privacy and AI-behaviour impact where relevant;
- exact implementation/release evidence used;
- required reviewers;
- validation performed;
- remaining open decisions or residual risks.

Do not hand a documentation proposal directly to Codex or Lovable as implementation authority until Orchestration has reconciled it into an approved issue or implementation brief.

## Documentation standards

- Use Markdown for written documentation.
- Give material documents clear titles, owners, version, status and update date.
- Distinguish implemented, controlled-beta, prototype, planned and prohibited capability.
- Keep exact revisions, schema versions, issue numbers and workflow-run IDs accurate.
- Use relative links for files within this repository.
- Record significant architecture decisions as ADRs when the decision is genuinely cross-cutting and durable; do not create speculative ADRs for unapproved future scope.
- Keep diagrams in source form and export presentation-ready versions where useful.
- Update linked documents when a decision changes.
- Do not duplicate executable application detail that belongs in `teammatesiq/platform`.

## Current non-negotiable boundary

Unless an approved Founder decision and updated baseline say otherwise:

- Admin TeamMate is the only SME v1 TeamMate.
- Lifecycle is Configuring → Probation → Active → Suspended → Archived.
- Paused maps to `suspended/customer_paused`.
- Current Microsoft access is delegated `Mail.Read` and `Calendars.Read` only.
- No Microsoft write permission, file authority or consequential external action is enabled.
- Production launch is not approved.

## Security and privacy

Do not commit passwords, API keys, access tokens, private keys, customer content, personal data, customer-confidential information or production datasets.

Release evidence should be metadata-only and content-free unless a separately approved secure evidence process explicitly requires otherwise.