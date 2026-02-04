# Minimum Requirements per Class

## Purpose
This page defines the minimum artifact requirements, validity windows, and review cadence per risk class.

Minimum requirements are **normative baselines**. Scopes may adopt stricter values; never weaker.

## Class A - Minimum GTAF set
**Required**
- [SB](../02-artifacts/system-boundary.md)
- [DR](../02-artifacts/decision-record.md)
- [RB](../02-artifacts/responsibility-binding.md) if delegation is semi/autonomous (optional for assistive)
- [DRC](../02-artifacts/delegation-readiness-check.md) for any semi/autonomous activation

**Validity & cadence**
- Review cycle: annual or event‑based
- Escalation path must exist (may be simple)
- [EIS](../02-artifacts/emergency-intervention-system.md) optional (recommended if time‑to‑harm < 1 day)

**Operational add‑ons**
- [DRB](../02-artifacts/decision-review-board.md) optional
- [DVM](../02-artifacts/decision-velocity-metrics.md) optional

## Class B - Elevated governance rigor
**Required**
- SB with explicit included/excluded and interface list
- DR with strict impact limits and expiry policy
- RB mandatory for any delegation beyond assistive
- DRC mandatory for activation; validity window must be bounded
- DRB mandatory review regime
- EIS mandatory if time‑to‑harm is short or rollback is slow
- Evidence and reachability requirements per [Evidence & Reachability Rules](../03-rules/evidence-and-reachability.md)

**Validity & cadence**
- Review cycle: at least quarterly
- DRC validity window: typically 30–90 days or event‑based
- Escalation reachability MUST be verified (evidence references)

**Operational add‑ons**
- DVM baseline recommended

## Class C - Mission-critical structural discipline
**Required (non‑negotiable)**
- SB with legal/org mapping and enforceability expectations
- DR with rigorous boundaries, excluded actions, explicit exception policy
- RB with mandate origin, outcome owner, escalation owner, handover rules
- DRC as a strict gate with a short validity window
- DRB formal regime with drift signals and explicit outputs
- EIS mandatory with reachable activation mechanism
- DVM mandatory baseline with thresholds and reporting cadence
- Evidence and reachability requirements per [Evidence & Reachability Rules](../03-rules/evidence-and-reachability.md)

**Validity & cadence**
- Review cycle: at least monthly (or tighter if time‑to‑harm is immediate)
- DRC validity window: typically 7–30 days or strictly event‑based
- Any meaningful change triggers immediate revalidation

**Reachability requirements**
- Escalation and intervention reachability MUST be demonstrated as evidence
- “Reachable under stress” is the assumption, not “reachable in theory”

## Validity windows & review cadence (summary)
Table T‑01 — Validity Windows & Review Cadence

| Class | Review cycle | DRC validity window (typical) | DRB required | EIS required | DVM baseline |
| --- | --- | --- | --- | --- | --- |
| A | Annual / event‑based | Event‑based / up to 90 days | Optional | Optional | Optional |
| B | Quarterly | 30–90 days / event‑based | Mandatory | Conditional → often mandatory | Recommended |
| C | Monthly (or tighter) | 7–30 days / event‑based | Mandatory | Mandatory | Mandatory |

The numbers above are **normative defaults**. Scopes may adopt stricter values; never weaker.
