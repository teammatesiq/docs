---
Title: ADR-014 Microsoft Email Send and Reconciliation
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Data & Integrations Lead
Implements: PD-005, ATC-005
---

# Context

Microsoft Graph `sendMail` returns `202 Accepted` with no response body. That confirms request acceptance, not completed processing or recipient delivery. A timeout can leave TMOS unable to know whether Graph received the request.

# Decision

1. TMOS owns the immutable prepared payload and uses `POST /v1.0/me/sendMail` in the bound Owner connection context.
2. Sent Items saving remains enabled. The adapter never creates an Outlook draft.
3. The attempt state machine is `prepared -> awaiting_approval -> approved -> submitted -> sent | indeterminate`, with explicit rejected, cancelled and known-failure outcomes.
4. `202 Accepted` moves the attempt only to `submitted`.
5. `sent` requires an unambiguous Sent Items match within the bounded reconciliation window defined in the Microsoft Integration Contract.
6. TMOS never claims `delivered` in SME v1.
7. Submitted and indeterminate attempts are never automatically retried. A user-initiated replacement is a new payload, approval and attempt.
8. A failure proven to occur before request transmission may be retried by the worker using the same attempt key while the approval is valid. Any uncertainty after transmission prohibits retry.
9. Suspension after provider invocation cannot recall the message; reconciliation may continue only to report the already-submitted outcome.
10. Provider correlation, response class, times, reconciliation queries and evidence references are audited without access tokens or unnecessary message content.

# Reconciliation

Matching uses the immutable mailbox identity, recipient sets, subject, canonical content digest/approved content evidence, attachment metadata, attempt correlation marker where supported, and a bounded time window. Zero or multiple credible matches become `indeterminate`. Provider-normalised content must be proven in the test tenant before a digest comparison is relied upon.

# Customer semantics

| Internal state | Customer meaning |
|---|---|
| approved | Ready for controlled submission; not sent |
| submitted | Microsoft accepted the request for processing |
| sent | Matching evidence exists in Sent Items; not proof of delivery |
| indeterminate | TMOS cannot safely determine the provider outcome |

# Consequences

- Work Queue Completed cannot be based on `202 Accepted`.
- The adapter must classify failures as definitely pre-transmission or uncertain; generic retry middleware is prohibited around sendMail.

# Acceptance evidence

- Contract tests for 202, 4xx, 429, 5xx, timeout and lost response.
- Duplicate-prevention, ambiguous-match and no-match tests.
- Test-tenant proof of reconciliation fields and provider normalisation.

# References

- [Microsoft Graph sendMail](https://learn.microsoft.com/en-us/graph/api/user-sendmail?view=graph-rest-1.0)

