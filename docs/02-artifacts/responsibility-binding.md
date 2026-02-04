# Responsibility Binding (RB)

## Purpose
Binds outcome ownership to a role and mandate for one or more DRs. Systems may act, but accountability remains human/organizational.

## Minimum fields (normative)
- `rb_id`
- `applies_to` (DR IDs)
- `owning_role` (outcome owner)
- `mandate_origin` (board resolution / governance charter)
- `delegation_rights` (whether/how delegation is permitted, boundaries)
- `escalation_owner` (who owns responsibility in exceptions)
- `validity_review_cycle`

## Example (non-binding, tool-agnostic)
```yaml
rb_id: RB-009
applies_to: [DR-0127]
owning_role: Product Lead (Support Platform)
mandate_origin: BR-2025-11
delegation_rights:
  allowed: true
  scope_limit: refund_decisions_under_500
escalation_owner: Head of Ops
validity_review_cycle: QUARTERLY
gtaf_ref:
  version: GTAF-0.1
status: ACTIVE
valid_from: 2026-01-01T00:00:00Z
valid_until: 2026-12-31T23:59:59Z
revision: 1
```

## Normative statement
No semi‑autonomous or autonomous execution without an active RB.

## Key references
- [Outcome Ownership](../10-terminology/glossary/#outcome-ownership)
- [Mandate](../10-terminology/glossary/#mandate)
- [Decision Record (DR)](../02-artifacts/decision-record/)
