# Decision Record (DR)

## Purpose
Defines a **delegable decision space** with authority, boundary, triggers, escalation, and validity. A DR does not merely record "what was decided"; it specifies **what may be delegated** and under which constraints.

## Minimum fields (normative)
- `dr_id`
- `decision_type` (POLICY | DELEGATION | AUTOMATION; list allowed)
- `decision_scope` (bound to SB and scope)
- `authority_role` (role, not person)
- `mandate_source`
- `decision_boundary`:

  - allowed actions
  - explicitly excluded actions
  - impact limits (budget, data class, risk)
- `delegation_level` (ASSISTIVE | SEMI_AUTONOMOUS | AUTONOMOUS)
- `trigger_conditions`
- `escalation_path` (including reachability)
- `valid_from`, `valid_until` (or `review_cycle`)

## Example (non-binding, tool-agnostic)
```yaml
dr_id: DR-0127
decision_type: [AUTOMATION]
scope:
  id: SCOPE-REFUNDS-CIP
  kind: DECISION_DOMAIN
  boundary_ref: SB-004
decision_scope:
  boundary_ref: SB-004
authority_role: Head of Customer Ops
mandate_source: GC-REFUNDS-01
decision_boundary:
  allowed_actions: [issue_refund]
  excluded_actions: [chargeback, payment_rail_access]
  impact_limits:
    max_refund_eur: 500
    data_class: PII_RESTRICTED
delegation_level: AUTONOMOUS
trigger_conditions: [complaint_category_x, transaction_verified]
escalation_path:
  - role: Support Lead
    within: 4h
  - role: Head of Ops
    within: 1h
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-01-01T00:00:00Z
valid_until: 2026-12-31T23:59:59Z
revision: 1
```

## Key rules
- Missing escalation or exclusions makes a DR incomplete.
- Delegation level determines whether an [RB](/02-artifacts/responsibility-binding/) is mandatory.
- DR defines **permission to delegate**, not a meeting outcome.

## Key references
- [Delegation](/10-terminology/glossary/#delegation)
- [Delegation Level](/10-terminology/glossary/#delegation-level)
- [Authority](/10-terminology/glossary/#authority-decision-authority)
- [Mandate](/10-terminology/glossary/#mandate)
- [System Boundary (SB)](/02-artifacts/system-boundary/)
