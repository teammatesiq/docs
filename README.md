# TeamMatesIQ Documentation

This repository is the canonical source for TeamMatesIQ product, architecture, trust, experience, commercial and evaluation intent.

Production application code, migrations, infrastructure and executable assurance live in [`teammatesiq/platform`](https://github.com/teammatesiq/platform). The Lovable repository is a non-authoritative customer-experience reference.

## Start here

- [Canonical document register](docs/README.md)
- [Delivery operating model](docs/governance/delivery-operating-model.md)
- [SME v1 current release boundary](docs/governance/sme-v1-current-release-boundary.md)
- [Cross-repository baseline manifest](docs/governance/cross-repository-baseline-manifest.md)
- [Consistency audit — 19 August 2026](docs/governance/consistency-audit-2026-08-19.md)
- [Admin TeamMate workflows](docs/product/admin-teammate-workflows.md)
- [Engineering release plan](docs/engineering/engineering-release-plan.md)
- [Test and evaluation specification](docs/engineering/test-evaluation-specification.md)

## Current controlled position

- Admin TeamMate is the only SME v1 TeamMate.
- The deployed lifecycle is Configuring → Probation → Active → Suspended → Archived.
- Customer-facing Paused maps to `suspended/customer_paused`.
- The pinned internal-alpha application candidate is recorded in the baseline manifest.
- Current Microsoft permissions are delegated `Mail.Read` and `Calendars.Read` only.
- No Microsoft write permission, file authority or consequential external action is enabled.
- Production launch remains a separate Founder decision.

Broader future-looking capability in a Draft specification is not implementation or activation authority. Use the current release-boundary record for the exact controlled scope.

## Repository structure

- `docs/strategy/` — product and commercial strategy
- `docs/architecture/` — platform, system, domain and TeamMate architecture
- `docs/product/` — Admin TeamMate role, workflows and onboarding
- `docs/ux/` — customer experience and interface requirements
- `docs/security/` — security, privacy and governance
- `docs/engineering/` — data, API, release and evaluation specifications
- `docs/brand/` — brand, messaging, terminology, claims and visual identity
- `docs/governance/` — authority, baseline, release-boundary and audit controls
- `engineering/backlog/` — approved planning artefacts
- `assets/` — approved brand and diagram assets

## Working principles

- GitHub is the durable decision and evidence record; chat history is working context only.
- Begin material work from a controlling issue and the relevant canonical references.
- Keep current release scope separate from target-state capability.
- Use pull requests for substantive changes.
- Update the register and baseline controls when a material decision changes.
- Never commit secrets, credentials, customer content or personal data.

See [CONTRIBUTING.md](CONTRIBUTING.md) and [AGENTS.md](AGENTS.md) before making changes.