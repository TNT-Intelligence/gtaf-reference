# Classification Criteria

## Purpose
This page specifies the normative criteria for assigning risk class per scope and decision domain.

## Normative rule
Risk class MUST be determined using the criteria below, assessed per scope and per decision domain.

## C1 - Impact domain (what can be harmed)
- Financial: potential monetary loss or unauthorized transfers
- Safety: physical harm risk
- Rights & legal status: eligibility, access, employment, sanctions
- Data: confidentiality/integrity of sensitive or regulated data
- Continuity: ability of the organization to operate
- Reputation: public trust damage and downstream consequences

## C2 - Magnitude (how large)
- maximum potential loss (bounded/unbounded)
- number of affected users/entities
- systemic coupling (single subsystem vs platform‑wide)

## C3 - Reversibility (how recoverable)
- rollback feasible within minutes/hours/days?
- harm fully undoable or only partially mitigable?
- external/legal facts created (contracts, reporting)?

## C4 - Time-to-harm (how fast)
- immediate harm possible (seconds/minutes)
- delayed harm (hours/days), allowing human intervention

## C5 - Control surface (how bounded)
- boundaries enforceable and narrow?
- escalation and kill‑switch paths reachable under stress?
- observability/traceability required

## C6 - Delegation level (autonomy amplifier)
- assistive
- semi‑autonomous
- autonomous

Higher autonomy MUST shift classification upward unless compensated by strict boundaries and low impact.

## C7 - Regulatory environment
- regulated industry, regulated data, critical infrastructure
- contractual liability and external audit exposure

## Normative rule
A scope MUST be Class C if any criterion indicates severe/irreversible harm potential with insufficient recovery time or high regulatory/legal consequence.
