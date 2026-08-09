---
Title: ADR-013 Controlled-action Approval Integrity
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Security & Governance Lead
Implements: PD-005, ATC-004
---

# Context

The only SME v1 controlled external write is email sending. Human approval must authorise the exact payload and cannot be inferred, reused or altered by model reasoning.

# Decision

1. A prepared email has immutable, monotonically versioned payload records. Editing creates a new version.
2. Canonical JSON uses UTF-8, deterministic key ordering and explicit arrays. Recipients are normalised for comparison, deduplicated and sorted by recipient type then canonical address; display names are retained for presentation.
3. Subject and body bytes, content type and line endings are preserved exactly as approved. Attachments bind identifier, filename, media type, size and SHA-256 content digest.
4. The SHA-256 approval digest covers Organisation, TeamMate, workflow, action, sender, recipients, subject, body, attachments, thread reference, policy/permission/Blueprint/DNA/workflow versions and `control_epoch`.
5. The authenticated Organisation Owner is the only eligible approver. TMOS records the server-resolved Owner identity and session assurance.
6. Approval expires 15 minutes after approval and earlier on any bound-value or authority change. An expired or stale approval never revives.
7. Approve and reject are mutually exclusive, concurrency-safe terminal decisions for one approval version.
8. Approval does not invoke Graph. A separate controlled-action service consumes it once after rechecking every bound control.
9. Consumption and creation of a unique action-attempt record occur atomically before provider invocation. The approval cannot authorise another attempt.
10. The UI receives the server-rendered approval view and digest/version token; it cannot substitute hidden fields.

# Canonicalisation contract

The implementation must publish language-independent test vectors containing input payload, canonical byte sequence and expected digest. Unicode is normalised to NFC for identity fields; body content is not semantically rewritten. Null, absent and empty values are distinct where the payload contract distinguishes them.

# Failure semantics

| Condition | Result |
|---|---|
| Payload changed | Prior approval stale; new approval required |
| Authority, epoch, policy or permission changed | Fail closed; approval stale |
| Competing decision | One commit wins; the other returns deterministic conflict |
| Attempt already exists | Return existing attempt; never invoke provider again |

# Consequences

- “Looks similar” is never payload equivalence.
- Template regeneration, recipient reordering before canonicalisation or attachment replacement can require renewed approval.

# Acceptance evidence

- Immutable schema and cryptographic test vectors.
- Edit, expiry, replay, bypass and concurrent decision tests.
- Hidden-field and cross-tenant approval mutation tests.

