---
Title: ADR-016 Selected Knowledge Access and ACL Lineage
Status: Proposed
Date: 2026-08-09
Owners: Head of Software / Solution Architect; Data & Integrations Lead; Security & Governance Lead
Implements: PD-003, PD-007, ATC-007
---

# Context

Microsoft consent alone must not grant TMOS access to every file the Owner can access. Selected permissions require both OAuth consent and an explicit resource assignment, while the Owner's native authority still limits effective access.

# Decision

1. Knowledge-source access is delegated, read-only and deny-by-default.
2. The runtime application must not request `Files.Read.All`, `Files.ReadWrite.All`, `Sites.Read.All` or `Sites.ReadWrite.All`.
3. Use the narrowest supported delegated Selected scope: `Files.SelectedOperations.Selected`, `ListItems.SelectedOperations.Selected`, `Lists.SelectedOperations.Selected` or `Sites.Selected`.
4. Each resource receives an explicit `read` assignment to the runtime application. A broader role is prohibited.
5. Provisioning is a separate customer-administrator bootstrap operation. The runtime application does not receive broad permissions merely to grant itself access.
6. Effective access requires both the application assignment and current Owner authority. Failure of either check blocks ingestion and retrieval.
7. Source records bind provider tenant, site, drive/list/item identifiers, selected-scope type, assignment evidence, Owner authority evidence, sensitivity class, version/change token, connection version and ingestion state.
8. Every chunk retains source ID, source version, ACL lineage and content digest. Retrieval verifies current source status, connection version, assignment and freshness before returning content.
9. Source removal immediately makes source and chunks non-retrievable, cancels sync, attempts assignment revocation and records a lineage-preserving tombstone.
10. If selected permissions cannot be provisioned and validated, the source is unavailable. Scope widening requires new Product, Security, Legal and Programme approval.

# Resource hierarchy rule

Prefer file/item, then folder/list, then site scope only where smaller scopes are not operationally supported for the approved source. The reason for any site-level assignment must be recorded and reviewed.

# Consequences

- Customer administrator involvement may be required during beta onboarding.
- Vector similarity is never an authorisation mechanism.
- Source deletion and derived-content deletion follow Legal retention decisions; retrieval denial is immediate regardless of retention.

# Acceptance evidence

- Non-production proof for each enabled Selected scope and assignment API/process.
- Owner-loses-access, assignment-revoked, source-removed and stale-chunk tests.
- Negative tests proving content from an unassigned or different-tenant source cannot be retrieved.

# Reference

- [Microsoft Selected permissions overview](https://learn.microsoft.com/en-us/graph/permissions-selected-overview)

