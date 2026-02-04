# Reference Case (High Risk)

**Case ID:** CASE-002 — Payment Authorization / Core Rail Control (Class C)

## Intent
Demonstrate mission‑critical delegation where the cost of failure is catastrophic and the kill‑switch must remain reachable under degraded conditions.

## Risk class
- Class C (non‑negotiable) due to systemic financial and legal impact and fast time‑to‑harm.

## Scope
- `scope.id`: SCOPE-PAYMENTS-RAIL
- `scope.kind`: SYSTEM_DOMAIN (or DECISION_DOMAIN anchored to rail SB)
- `scope.boundary_ref`: SB-101

## System Boundary (SB-101 - Payment Rail Gateway)
- Included: payment gateway, authorization service, transaction signing module
- Excluded: customer support tooling, analytics, experimentation systems
- Allowed interfaces:

  - authorized transaction submission API
  - status query API (read‑only)
- Forbidden:

  - any interface from non‑authorized domains
  - direct operator shell access (unless emergency procedure)
- Data spaces:

  - transaction data (regulated)
  - keys/signing material (highest sensitivity)
- Legal/org mapping:

  - gateway owned by Entity A; regulated operations owned by Entity A under compliance obligations

## Decision Record (DR-9001 - Transaction Authorization Delegation)
- Type: POLICY + AUTOMATION (policy defines allowed automation)
- Authority role: CISO (or equivalent governance authority)
- Mandate source: PAY-CHARTER-01
- Boundary:

  - Allowed: authorize transactions only within pre‑approved rule set
  - Excluded: policy changes to authorization rules; key access; signing module changes
  - Impact limits: strict max exposure per time window; strict anomaly controls
- Delegation level: SEMI_AUTONOMOUS or AUTONOMOUS (depending on design)
- Trigger conditions: inbound authorized requests; anomaly thresholds
- Escalation path:

  - On‑Call Security Officer within 15 minutes
  - Head of Ops within 10 minutes
  - Executive Authority (board delegate) within 30 minutes
- Expiry policy: event‑based + monthly review

## Responsibility Binding (RB-9001 - Rail Outcome Ownership)
- Applies to: DR-9001
- Outcome owner: Head of Payments Operations
- Mandate origin: BR-EXEC-2026-01
- Escalation owner: CISO
- Handover rules: explicit continuity for on‑call rotations and executive coverage

## Decision Review Board (DRB-9001)
- Scope: SCOPE-PAYMENTS-RAIL
- Frequency: monthly (or bi‑weekly if time‑to‑harm is immediate)
- Coverage: DR-9001 family + related DRCs + drift signals
- Outputs: revalidate, amend DR/RB, suspend delegation, trigger EIS, issue new DRC

## Emergency Intervention / Kill-Switch (EIS-9001 - Rail Hard Stop)
- Scope: SB-101 (entire boundary) + optional narrower target stops
- Activation authority: CISO and Head of Ops (dual authority if required)
- Mandate ref: PAY-CHARTER-01
- Mechanism requirements:

  - reachable under partial outage
  - must not depend on the failing authorization service itself
  - executable within minutes
- Duration: until revalidated
- Re‑enable conditions: DRB approval + new DRC issuance

## Decision Velocity Metrics (DVM-9001 - Rail Integrity Signals)
- Cadence: daily reporting + alert thresholds
- Metrics:

  - delegations without valid DRC (must be 0)
  - time‑to‑EIS activation in drills (must meet threshold)
  - DRB overdue items (must be 0)
  - anomaly overrides count and rationale coverage

## Delegation Readiness Check (DRC-9001 - Rail Delegation Permissibility)
- Target: SYSTEM:AuthorizationService
- Context: SB-101, DR-9001, RB-9001
- Required:

  - SB/DR/RB ACTIVE + valid
  - DRB regime defined and active
  - EIS defined + reachability verified
  - DVM baseline defined + thresholds mapped to actions
- Evidence required (non‑negotiable):

  - mandate documentation
  - escalation procedure + coverage model
  - EIS drill record (practical activation evidence)
  - DRB meeting record references
- Result: PERMITTED only within short validity window (e.g., 7–30 days)

## Conformity claim (canonical)
`(SCOPE-PAYMENTS-RAIL, GTAF-0.1, 2026-02-01..2026-02-28, basis: DRC-9001)`

## Revalidation triggers
- any boundary/interface change
- any authority/mandate change
- any incident involving drift/anomaly
- any EIS reachability evidence expiration
- any DVM threshold breach requiring intervention
- any delegation level change

## Key references
- [SB](../02-artifacts/system-boundary.md)
- [DR](../02-artifacts/decision-record.md)
- [RB](../02-artifacts/responsibility-binding.md)
- [DRC](../02-artifacts/delegation-readiness-check.md)
- [DRB](../02-artifacts/decision-review-board.md)
- [EIS](../02-artifacts/emergency-intervention-system.md)
- [DVM](../02-artifacts/decision-velocity-metrics.md)
