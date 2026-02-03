# Claim Index (Operational Overview, Tool-Agnostic)

## Purpose
The Claim Index provides a single, operational overview of all active and historical GTAF conformity claims. It is designed for quick navigation (“What is currently permitted, where, and until when?”) while remaining strictly reference‑driven (claims link to DRCs, which link to artifacts and evidence).

**Normative rule:** the Claim Index must never replace the claim objects themselves. It is a curated overview that must link to the canonical claim records.

## Recommended structure (page layout)

### 1) Active claims (primary table)
A table listing all claims that are currently valid (today ∈ validity window) and not revoked.

**Columns (recommended):**
- Claim ID (link to claim page/section)
- Scope (scope.id + scope.kind; link to Scope Record)
- Boundary Anchor (SB‑ID; link)
- Risk Class (A/B/C)
- Reference Version (GTAF‑x.y)
- Validity (valid_from → valid_until)
- Status (ACTIVE / EXPIRING / BLOCKED)
- Basis (DRC IDs) (links to DRCs)
- Targets Covered (short list)
- Owner (Role) (issuer.role or scope owner)
- Notes / Limitations (short)

**Operational status rules (simple, useful):**
- ACTIVE: validity > 14 days remaining and no known blockers
- EXPIRING: validity ≤ 14 days remaining (or ≤ 7 for Class C)
- BLOCKED: any referenced DRC is NOT_PERMITTED or evidence expired

You can maintain the status manually or define a simple rule‑of‑thumb—no tooling required.

### 2) Claims needing action (action queue)
A short section listing:

- claims expiring soon
- claims with overdue reviews
- claims blocked due to missing/expired evidence
- scopes with delegation but no active claim

**Format (recommended):**
- Bullet list with: Claim ID, reason, required action, due date, owner role

### 3) Historical claims (archive table)
A separate table for claims that are expired or revoked. Keep it lean; the value is traceability.

**Columns (recommended):**
- Claim ID
- Scope
- Risk Class
- Validity window
- End state: EXPIRED / REVOKED
- Revocation reason (if revoked)
- Replacement claim (if any)

## Canonical claim record pattern (Confluence-friendly)
Create one page (or one section) per claim using a consistent structure:

**Header block (always)**
- Claim ID: …
- Scope: …
- Boundary Anchor: …
- Risk Class: …
- Claim Type: Delegation Conformity / Structural (No Delegation)
- GTAF Reference Version: …
- Validity Window: …
- Issuer Role: …
- Issued At: …

**Basis**
- DRC IDs: …
- Artifact Set (closure): list of IDs
- Delegation Targets: list

**Evidence**
- list of evidence refs (mandates, procedures, tests, logs)

**Limitations / Exclusions**
- explicit bullets

**Lifecycle Notes**
- triggers for revalidation
- renewal plan (who/when)
- revocation conditions

## Minimal example (index row)
- Claim ID: CLAIM-PAYMENTS-RAIL-2026-02
- Scope: SCOPE-PAYMENTS-RAIL (SYSTEM_DOMAIN)
- SB: SB-101
- Class: C
- Ref: GTAF-0.1
- Validity: 2026-02-01 → 2026-02-28
- Status: EXPIRING
- Basis: DRC-9001
- Targets: AuthorizationService
- Owner: CISO
- Notes: “Excludes policy changes; requires monthly DRB + EIS drill evidence”

## Guardrails (avoid common Confluence drift)
- Do not add “compliance score” columns.
- Do not convert the index into a narrative status report.
- Do not list claims without links to DRCs and scope/boundary anchors.
- Do not allow “global claims” rows—every row must have scope + version + time window.
