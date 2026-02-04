# Reference Case (Lower Risk)

**Case ID:** CASE-001 — Refund Delegation Policy (Class A/B)

## Intent
Demonstrate a bounded financial decision domain where delegation is permitted under strict impact limits and clear reversibility.

## Risk class
- Default: Class A if strictly low threshold and immediate reversal exists
- Escalates to Class B if refund volume is material, rollback is slow, or scope spans multiple systems

## Scope
- `scope.id`: SCOPE-REFUNDS-CIP
- `scope.kind`: DECISION_DOMAIN
- `scope.boundary_ref`: SB-004 (Customer Interaction Platform)

## System Boundary (SB-004)
- Included: CRM core, refund workflow engine, customer history DB
- Excluded: billing ledger core, payment rail gateway
- Allowed interfaces: CRM API read/write; refund engine API invoke; customer history read
- Forbidden interfaces: direct payment rail access; billing ledger write
- Data spaces: PII (restricted), interaction logs (internal), refund events (internal)
- Legal/org mapping: CRM owned by Entity A; refund engine owned by Entity A

## Decision Record (DR-0127 - Refund Delegation)
- Type: AUTOMATION
- Authority role: Head of Customer Ops
- Mandate source: GC-REFUNDS-01
- Boundary:

  - Allowed: issue refund <= EUR 500
  - Required conditions: loyalty_score > 0.8 AND fraud_risk < threshold
  - Excluded: chargebacks; refunds > EUR 500; any action touching payment rails
- Delegation level: AUTONOMOUS
- Trigger conditions: customer complaint category X; verified transaction ID
- Escalation path:

  - Support Lead (P2) within 4h
  - Head of Ops (P1) within 1h
- Expiry policy: REVIEW_CYCLE quarterly (Class B) or annual (Class A)

## Responsibility Binding (RB-009 - Refund Outcome Ownership)
- Applies to: DR-0127
- Outcome owner: Product Lead (Support Platform)
- Mandate origin: BR-2025-11
- Escalation owner: Head of Ops
- Delegation permissions: no sub‑delegation beyond defined agent target

## Delegation Readiness Check (DRC-045 - SupportBot Refund Delegation)
- Target: AGENT:SupportBot
- Context: SB-004, DR-0127, RB-009
- Required artifacts: SB-004, DR-0127, RB-009
- Evidence required:

  - mandate refs (GC-REFUNDS-01, BR-2025-11)
  - escalation procedure reference
- Result:

  - PERMITTED if evidence is valid and reachability confirmed (Class B)
  - NOT_PERMITTED if escalation reachability is unverified or expired

## Evidence map (minimal)
- EVID-MANDATE-01: GC-REFUNDS-01 (authority mandate)
- EVID-MANDATE-02: BR-2025-11 (RB binding)
- EVID-ESC-01: escalation procedure doc reference
- EVID-TEST-01 (Class B only): escalation reachability drill record

## Conformity claim (canonical)
`(SCOPE-REFUNDS-CIP, GTAF-0.1, 2026-01-01..2026-03-31, basis: DRC-045)`

## Revalidation triggers
- Threshold change (> EUR 500)
- Scope expands to billing/payment rails
- Delegation target changes
- Role/mandate changes (authority/outcome owner)
- Escalation coverage model changes

## Key references
- [SB](../02-artifacts/system-boundary/)
- [DR](../02-artifacts/decision-record/)
- [RB](../02-artifacts/responsibility-binding/)
- [DRC](../02-artifacts/delegation-readiness-check/)
