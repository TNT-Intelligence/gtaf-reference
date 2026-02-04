# Decision Velocity Metrics (DVM)

## Purpose
Measures whether decision speed is outpacing structural integrity. DVM is not a performance KPI; it is an early warning system against structural decay.

## Examples (non‑binding)
- Ratio of implicit decisions without DR
- Time between decision introduction and RB binding
- Delegations without valid DRC
- Frequency of EIS activations per domain
- DRB review backlog per scope

## Example (non-binding, tool-agnostic)
```yaml
dvm_id: DVM-9001
scope:
  id: SCOPE-PAYMENTS-RAIL
  kind: SYSTEM_DOMAIN
  boundary_ref: SB-101
cadence: DAILY
metrics:
  - name: delegations_without_valid_drc
    threshold: 0
  - name: time_to_eis_activation_drill
    threshold: 2m
  - name: drb_overdue_items
    threshold: 0
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-02-01T00:00:00Z
valid_until: 2026-03-01T00:00:00Z
revision: 1
```

## Key references
- [Decision Debt](../10-terminology/glossary.md#decision-debt)
- [DRB](../02-artifacts/decision-review-board.md)
