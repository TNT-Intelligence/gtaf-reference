# Relation to IAM and Zero Trust

## Core distinction
Zero Trust focuses on **access trust** (who/what may access which resource, under which conditions). GTAF focuses on **decision trust**: who is authorized to define delegable decision spaces, where those decisions apply, who owns outcomes, and how intervention remains reachable.

## How GTAF complements Zero Trust
- Zero Trust answers **connection and access**.
- GTAF answers **decision authority** within explicit [boundaries](/02-artifacts/system-boundary/) and [scope](/10-terminology/glossary/#scope).
- Zero Trust enforces access policies; GTAF ensures the **authority to define those policies** is legitimate and bounded.

## Structural bridge
GTAF can be viewed as **"zero trust for authority"**:

- [Decision Records](/02-artifacts/decision-record/) define what may be delegated.
- [Responsibility Bindings](/02-artifacts/responsibility-binding/) keep outcome ownership explicit.
- [DRC](/02-artifacts/delegation-readiness-check/) provides a binary gate before delegation.

## Guardrail
GTAF does not replace IAM or Zero Trust. It formalizes the **delegation semantics** that sit upstream of enforcement.
