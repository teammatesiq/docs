---
Title: ADR-015 Delegated Microsoft Access and Consent
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Data & Integrations Lead; Security & Governance Lead
Implements: PD-007, ATC-006
---

# Context

SME v1 serves one authenticated Organisation Owner using one eligible Microsoft 365 work or school identity. Application-only and shared-mailbox access would exceed the approved authority boundary.

# Decision

1. Use the Microsoft identity platform v2 authorisation-code flow with PKCE and server-side token exchange/storage.
2. The authority endpoint is organisation-only; consumer Microsoft accounts are rejected. Tenant and subject claims are validated against the immutable connection identity.
3. The base delegated scope set is `openid profile offline_access User.Read Mail.Read Mail.Send Calendars.Read`.
4. Calendar write, shared-mailbox, shared-calendar and application permissions are prohibited.
5. Selected knowledge-source scopes are requested only when that source type is enabled and follow ADR-016 and the Microsoft Integration Contract.
6. Bind Organisation, TMOS Owner, Entra tenant ID, Entra object/subject identity, mailbox user ID and primary mailbox address. The connection cannot move between Organisations.
7. Refresh tokens are encrypted at rest, never returned to the client, rotated on refresh when Microsoft issues a replacement and invalidated on disconnect.
8. Before controlled execution, revalidate connection state, tenant, subject/mailbox, effective scopes, token health and lifecycle epoch.
9. Disconnect immediately adds `integration_disconnected`, increments the lifecycle epoch, stops dependent subscriptions/jobs and deletes or cryptographically destroys refresh capability.
10. Reconnection creates a new connection version and does not revive stale approvals or work.

# Registration boundary

Production, staging and development redirect URIs must be exact HTTPS allowlisted values recorded in the Microsoft Integration Contract. Wildcards, localhost in production and client-held secrets are prohibited. Hosting selection and actual URI values require a separate platform/hosting decision.

# Consequences

- Some customer tenants may require administrator consent under their policies even where Microsoft marks a delegated scope as not universally admin-required.
- `Mail.Read` is required for approved inbox work and Sent Items reconciliation; `Mail.Send` alone is insufficient for the full product contract.

# Acceptance evidence

- Test-tenant sign-in, refresh, consent and disconnect evidence.
- Wrong-tenant, consumer-account, shared-mailbox, missing-scope and revoked-consent tests.
- Proof that no application permission or client-side token path exists.

# References

- [Microsoft identity platform authorisation-code flow](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-auth-code-flow)
- [Microsoft Graph delegated access](https://learn.microsoft.com/en-us/graph/auth-v2-user)
- [Microsoft Graph permissions reference](https://learn.microsoft.com/en-us/graph/permissions-reference)

