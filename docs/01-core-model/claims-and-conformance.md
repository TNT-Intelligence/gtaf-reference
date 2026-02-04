# Claims and Conformance

Conformity in GTAF is **binary**, **scope‑bound**, and **time‑bound**. A claim without scope, reference version, and time window is invalid.

## Canonical claim format (normative)
**Conformity Claim = (Scope, GTAF Reference Version, Time Window, Evidence References)**

Minimum claim fields:

- `scope.id`
- `gtaf_ref.version`
- `valid_from`, `valid_until`
- `basis.drc_ids` (list of [DRC](../02-artifacts/delegation-readiness-check.md) IDs; required if delegation exists)
- `basis.artifact_set` (minimal closure set)
- `issuer.role`
- `issued_at`
- optional: `risk.class`

Without these fields, the claim is structurally undefined and must be treated as **marketing, not reference validity**.

## Structural meaning
A scope is GTAF‑conformant only if the **minimal formal artifact core** is satisfied:

- [SB](../02-artifacts/system-boundary.md) exists and decision is inside boundary.
- [DR](../02-artifacts/decision-record.md) exists for the decision space.
- [RB](../02-artifacts/responsibility-binding.md) binds outcome ownership to mandate and role.
- [DRC](../02-artifacts/delegation-readiness-check.md) is issuable and PERMITTED.
- Temporality and [risk class](../05-risk-and-criticality/risk-classes.md) requirements are satisfied.

## Two-layer versioning (reader guidance)
Conformity depends on **both** layers:

- **Reference layer:** which GTAF reference version defines meaning (`gtaf_ref.version`).
- **Implementation layer:** whether artifacts/claims are ACTIVE and within their validity windows.

Both must hold. A valid artifact set without a declared reference version is **not** conformant.

## Claim validity rules (normative)
- Claims expire automatically at `valid_until`.
- Any invalidation of a basis artifact invalidates the claim.
- Claims do **not** override artifacts; they summarize their structural state.
- Claims MUST specify the [reference version](../10-terminology/glossary.md#reference-version) used to interpret artifacts.

## Common invalid patterns
- Claim without scope or time window.
- Claim without reference version.
- Claim without DRC when any semi/autonomous delegation exists.
- Claim without evidence references where reachability is required.

## Key references
- [Conformity](../10-terminology/glossary.md#conformity-gtaf-conformant)
- [Reference Version](../10-terminology/glossary.md#reference-version)
- [Validity Window](../10-terminology/glossary.md#validity-window)
- [Versioning & Change Control](../11-versions/versioning-and-change-control.md)
- [Conformity Claim Format](../01-core-model/conformity-claim-format.md)
- [Claim-to-DRC Mapping](../01-core-model/claim-to-drc-mapping.md)
