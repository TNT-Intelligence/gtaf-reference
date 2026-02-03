# Conformity Claim Format

## Purpose
This page defines the **only valid format** for making “GTAF‑conformant” statements. GTAF conformity is not a general attribute of an organization or system; it is a **binary, scope‑bound claim** valid only relative to a GTAF reference version and a time window.

A conformity claim must be precise enough that an independent reviewer can determine whether it is true by checking the referenced artifacts and evidence—without relying on informal trust or narrative.

## Scope
This page specifies:

- the canonical claim schema
- how claims bind to scope, reference version, and validity window
- what evidence and DRC basis must be present
- examples for Class A/B/C scopes
- anti‑patterns and invalid claim forms
- minimal rules for claim lifecycle (issue, expire, renew, revoke)

Not in scope:

- certification, badges, maturity scores
- pricing/licensing terms beyond structural binding
- tool‑specific claim storage or issuance workflows

## Normative principles (binding)
- **CC1 — Conformity is binary, not graded:** a scope is either conformant (PERMITTED) or not (NOT_PERMITTED).
- **CC2 — Conformity is always bound to (Scope, Version, Time):** a claim without these bindings is structurally undefined and invalid.
- **CC3 — DRC is the basis of any claim involving delegation:** if semi/autonomous delegation exists, the claim MUST reference one or more DRCs.
- **CC4 — Claims do not override artifacts:** claims summarize artifact state; if artifacts become invalid, the claim is invalid.
- **CC5 — Evidence is required where reachability/authority is required:** claims must reference evidence objects proving these are valid and reachable.

## Canonical claim schema (normative)
A GTAF conformity claim MUST be representable as the following structured object.

**Required fields**
- `claim_id` (string) — unique claim identifier
- `scope.id` (string)
- `scope.kind` (enum) — LEGAL_ENTITY | ORG_UNIT | SYSTEM_DOMAIN | DECISION_DOMAIN
- `scope.boundary_ref` (SB-ID) — primary boundary anchor
- `gtaf_ref.version` (string)
- `risk.class` (enum) — A | B | C
- `valid_from` (date‑time)
- `valid_until` (date‑time)
- `basis.drc_ids` (list of DRC‑IDs) — required if any semi/autonomous delegation exists
- `basis.artifact_set` (list of artifact IDs) — minimal closure set (SB/DR/RB/…)
- `evidence_refs` (list of evidence IDs/refs) — required for Class B/C and for any claim with reachability requirements
- `issuer.role` (string) — role authorized to issue/declare the claim (not a person)
- `issued_at` (date‑time)

**Optional but recommended fields**
- `delegation_targets` (list) — explicit target contexts covered by the claim
- `limitations` (string/list) — explicit exclusions (“does not cover X”)
- `change_trigger_policy` (enum) — EVENT_BASED | REVIEW_BASED | HYBRID
- `related_rcr_ids` (list)
- `revocation` (object) — revocation reason + timestamp if revoked early

**Normative rule:** a claim MUST be invalidated if any referenced basis artifact becomes RETIRED or falls outside its validity window.

## Example (non-binding, tool-agnostic)
```yaml
claim_id: CLAIM-REFUNDS-2026Q1
scope:
  id: SCOPE-REFUNDS-CIP
  kind: DECISION_DOMAIN
  boundary_ref: SB-004
gtaf_ref:
  version: GTAF-0.1
risk:
  class: A
valid_from: 2026-01-01T00:00:00Z
valid_until: 2026-03-31T23:59:59Z
basis:
  drc_ids: [DRC-045]
  artifact_set: [SB-004, DR-0127, RB-009, DRC-045]
evidence_refs: [EVID-MANDATE-01, EVID-ESC-01]
issuer:
  role: Head of Customer Ops
issued_at: 2026-01-01T00:10:00Z
limitations:
  - excludes chargebacks
  - excludes refunds > EUR 500
status: ACTIVE
revision: 1
```

## Claim types (recommended taxonomy)

1. **Delegation Conformity Claim**

   - Covers delegation targets/decision domains based on DRC(s).

2. **Structural Conformity Claim (No Delegation)**

   - Permissible only if no semi/autonomous delegation exists in‑scope; basis is SB/DR/RB completeness and governance readiness, but must not imply permission to delegate.

## Minimal closure rules (artifact set completeness)
A claim’s `basis.artifact_set` MUST include:

- at least one SB
- all DRs covered by the claim
- all RBs binding those DRs (where required)
- all referenced DRCs (for delegation claims)
- for Class B/C: DRB and EIS if required by risk class rules
- for Class C: DVM baseline artifact, where mandatory

**Normative rule:** if the artifact set is not closed under references, the claim is invalid.

## Validity windows (normative defaults)
Claims must be time‑bounded. Default maximum validity by risk class (unless stricter scope rules apply):

- Class A: up to 90 days (or event‑based)
- Class B: 30–90 days (recommended), must not exceed quarterly review cadence
- Class C: 7–30 days (recommended), must be short and frequently revalidated

These are defaults; a scope may choose tighter windows but never longer than its required review regime.

## Examples (canonical)
**Example 1 — Class A (bounded refunds, reversible)**
- claim_id: CLAIM-REFUNDS-2026Q1
- scope: SCOPE-REFUNDS-CIP (DECISION_DOMAIN), boundary SB-004
- version: GTAF-0.1
- risk: A
- validity: 2026-01-01 .. 2026-03-31
- basis: DRC-045, artifacts: SB-004, DR-0127, RB-009, DRC-045
- issuer.role: Head of Customer Ops
- limitations: excludes chargebacks and refunds > EUR 500

**Example 2 — Class B (material operational impact)**
- shorter validity window; evidence references required
- escalation procedure evidence
- reachability test record evidence (recent)
- basis includes DRB if Class B requires it for this scope

**Example 3 — Class C (mission‑critical rail control)**
- validity: 7–30 days
- basis: DRC-9001
- artifacts: includes DRB, EIS, DVM
- evidence: mandate refs, escalation coverage model, EIS drill activation record, DRB records
- explicit delegation targets covered and excluded

## Claim lifecycle rules (normative)
**Issuance**
A claim may be issued only if:

- all basis artifacts are ACTIVE and within validity
- all required evidence references are valid and accessible
- DRC result is PERMITTED for all covered delegation targets

**Expiry**
Claims expire automatically at `valid_until`. Expired claims must not be used as proof of current conformity.

**Renewal**
Renewal requires:

- revalidation of required artifacts and evidence
- issuance of a new claim (new claim_id recommended), or incremented claim revision if you manage claims as artifacts

**Revocation (early invalidation)**
A claim MUST be revoked if:

- any basis artifact becomes invalid (expired/retired)
- an escalation or EIS reachability test fails
- a boundary expansion increases risk without reclassification
- an incident indicates drift beyond defined tolerance (Class B/C)
- evidence becomes unavailable or outdated

## Anti-patterns (invalid claim forms)
- **Global claims:** “We are GTAF compliant.” (missing scope/version/time)
- **Versionless claims:** “GTAF conformant within Payments.” (missing reference version)
- **Timeless claims:** “GTAF conformant since 2024.” (missing validity window)
- **Claim without DRC when delegation exists**
- **Evidence‑free reachability claims:** “Kill‑switch exists.”
- **Scope leakage:** using DRs/RBs from another scope without explicit linkage

## Minimal claim checklist (for authors)
Before publishing a claim, confirm:

1. Scope is explicit and boundary‑anchored (SB reference present)

2. GTAF reference version is specified

3. Validity window is bounded

4. Risk class is declared and consistent with scope

5. Basis artifact set is closed under references

6. DRC basis exists and is PERMITTED (if delegation exists)

7. Evidence references exist and are current (especially reachability in B/C)

8. Limitations/exclusions are explicit
