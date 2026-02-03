# System Boundary (SB)

## Purpose
Defines **where responsibility and liability apply and stop**. Without an SB, delegation is structurally undefined because accountability endpoints are missing.

SB is not an architecture diagram. It is a **liability and accountability edge** that makes the boundary explicit: what is inside, what is outside, and which interfaces are permitted.

## Minimum fields (normative)
- `sb_id` (stable identity)
- `name` / domain
- `boundary_types` (Operational, Data, Decision)
- `included_components`
- `excluded_components`
- `interfaces` (allowed interfaces / touchpoints)
- `legal_org_mapping` (component to legal/org owner)
- `data_boundary` (data spaces, classifications)
- `decision_rights` (which decisions may exist inside this boundary)

## Example (non-binding, tool-agnostic)
```yaml
sb_id: SB-004
name: Customer Interaction Platform Boundary
scope:
  id: SCOPE-REFUNDS-CIP
  kind: DECISION_DOMAIN
  boundary_ref: SB-004
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-01-01T00:00:00Z
valid_until: 2026-12-31T23:59:59Z
revision: 1
boundary_types: [OPERATIONAL, DATA, DECISION]
included_components: [crm_core, refund_engine, customer_history_db]
excluded_components: [payment_rail_gateway, billing_ledger_core]
interfaces: [crm_api_read_write, refund_engine_invoke, customer_history_read]
legal_org_mapping:
  - component: crm_core
    owner: Entity-A
data_boundary: [pii_restricted, interaction_logs_internal]
decision_rights: [refund_decisions_under_500]
```

## Semantics
- SB is the **responsibility edge** for governance, not a descriptive drawing.
- No delegation is valid if it is not clearly **inside** a boundary.

## Common failure modes
- Vague boundaries without explicit inclusions/exclusions
- Missing interface list (unclear allowed touchpoints)
- No ownership mapping to legal/org entities

## Key references
- [Scope](/10-terminology/glossary/#scope)
- [Decision Record (DR)](/02-artifacts/decision-record/)
