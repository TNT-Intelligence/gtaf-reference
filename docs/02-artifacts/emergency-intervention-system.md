# Emergency Intervention System (EIS)

## Purpose
Immediate, structural suspension of delegated authority inside an SB or for specific DRs.

## Minimum fields (normative)
- `eis_id`
- `scope` (SB/DR/target)
- `activation_authority` (who may activate; mandate)
- `activation_mechanism` (how reachable; how fast)
- `duration`
- `reenable_conditions`
- `post_incident_requirements` (e.g., DRB review, new DRC)

## Normative rule
EIS must be reachable under degraded conditions and must not depend on the failing subsystem.

## Key references
- [Reachability](../10-terminology/glossary.md#reachability)
- [Time‑to‑Harm](../10-terminology/glossary.md#time-to-harm)

## Example (non-binding, tool-agnostic)
```yaml
eis_id: EIS-9001
scope:
  boundary_ref: SB-101
  targets: [SYSTEM:AuthorizationService]
activation_authority: CISO
activation_mechanism:
  path: out_of_band_kill_switch
  max_time_to_activate: 2m
duration: until_revalidated
reenable_conditions: [drb_approval, new_drc]
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-02-01T00:00:00Z
valid_until: 2026-03-01T00:00:00Z
revision: 1
```
