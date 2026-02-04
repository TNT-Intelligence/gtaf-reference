# Decision Review Board (DRB)

## Purpose
Periodic review of decision drift and quality over time. DRB operates against artifacts and evidence, not opinions.

## Normative properties
- Periodic cadence (risk‑class dependent)
- Operates against SB/DR/RB/DRC, not narrative
- Triggers revalidation, adjustments, or EIS activation

## Example (non-binding, tool-agnostic)
```yaml
drb_id: DRB-9001
scope:
  id: SCOPE-PAYMENTS-RAIL
  kind: SYSTEM_DOMAIN
  boundary_ref: SB-101
cadence: MONTHLY
coverage:
  dr_ids: [DR-9001]
  drc_ids: [DRC-9001]
outputs_expected: [revalidate, amend, suspend, trigger_eis]
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-02-01T00:00:00Z
valid_until: 2026-03-01T00:00:00Z
revision: 1
```

## Key references
- [Decision Drift](../10-terminology/glossary.md#decision-drift)
- [DRC](../02-artifacts/delegation-readiness-check.md)
