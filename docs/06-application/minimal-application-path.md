# Minimal Application Path

GTAF is a **method for artifact creation**, not an implementation guide. The minimal path is the five‑pillar method.

## Five-pillar method (normative)

### Pillar 1 - System Capture
**Goal:** convert current state into explicit structure.

Primary artifact: [System Boundary (SB)](../02-artifacts/system-boundary.md)

Outputs:

- SB drafts + boundary rationale
- domain/system/interface inventory
- preliminary risk/criticality assignment

### Pillar 2 - Governance Definition
**Goal:** define decision spaces and make mandates visible.

Primary artifacts: [Decision Record (DR)](../02-artifacts/decision-record.md), [Responsibility Binding (RB)](../02-artifacts/responsibility-binding.md)

Outputs:

- DR catalogue (decision‑space centric)
- RB bindings (mandates/roles/escalation)
- ambiguity list: decision‑relevant but not mandated

### Pillar 3 - Architecture Binding
**Goal:** translate governance into technical guardrails **without implementation**.

Outputs:

- boundary enforcement requirements
- escalation/kill‑switch reachability requirements
- logging/traceability requirements (artifact‑based, tool‑agnostic)

### Pillar 4 - Documentation & Traceability
**Goal:** ensure explainability, handover readiness, and reconstructability.

Outputs:

- referential integrity (IDs, relations, versions)
- artifact history/change control
- ability to reconstruct “what applies and why”

### Pillar 5 - Trust & Readiness Review
**Goal:** formal validation of structural permissibility.

Primary artifact: [Delegation Readiness Check (DRC)](../02-artifacts/delegation-readiness-check.md)

Optional by [risk class](../05-risk-and-criticality/risk-classes.md):

- [DRB](../02-artifacts/decision-review-board.md) plan
- [EIS](../02-artifacts/emergency-intervention-system.md) definition
- [DVM](../02-artifacts/decision-velocity-metrics.md) baseline
