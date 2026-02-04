# Governance & Trust Architecture Framework (GTAF)

GTAF is a **normative reference framework** that makes decision authority, responsibility, and system boundaries explicit in complex technical environments. Instead of relying on prose, tacit expertise, or post‑hoc controls, GTAF defines a small set of **structured artifacts** that function as enforceable reality.

This reference is offered as a **proposed** normative baseline and is intended to be reviewed, tested, and iterated through controlled change.
It does **not** guarantee decision correctness; it defines structural prerequisites for delegation.

## What is new about GTAF
Unlike governance checklists or maturity models, GTAF makes delegation **binary and verifiable**.  
It binds every claim to **scope, version, and time**, and treats artifacts as **normative reality**, not documentation.
It is complementary to existing standards, but focuses on **structural delegation prerequisites** rather than control catalogs.

## Why GTAF (in 2 minutes)
If you face any of these, GTAF is for you:

- Delegation happens without clear accountability (who owns outcomes?).
- Boundaries are unclear or contested (what is inside/outside scope?).
- Escalation or kill‑switches exist “on paper” but are not reachable.
- Risk class decisions are debated without a shared structural baseline.

What GTAF changes:

- **Artifacts replace ambiguity**: SB/DR/RB/DRC make authority, responsibility, and boundaries explicit.
- **Delegation becomes binary**: PERMITTED or NOT_PERMITTED based on structure and evidence.
- **Time and scope are explicit**: claims expire; scope and version are required.

GTAF applies to **all delegation contexts**, not just high‑risk systems.  
Risk class determines **how strict** the requirements are, not whether GTAF applies at all.

Example (low risk):

- A SupportBot refund policy (Class A) still requires SB/DR/RB/DRC, but with lighter evidence and review cadence.

## Before vs After (mini example)
Before: “The agent can refund up to EUR 500 if it seems safe.”  
After: **SB** defines scope, **DR** defines allowed actions/limits, **RB** binds ownership, **DRC** gates activation.

## What GTAF is
- A reference model for **safe [delegation](10-terminology/glossary/#delegation)** in human, automated, and agentic systems.
- **Artifact‑centric**: decisions, boundaries, responsibility, and readiness are explicit objects with identity, [scope](10-terminology/glossary/#scope), and [validity windows](10-terminology/glossary/#validity-window).
- A **binary gate** for delegation: structurally **PERMITTED** or **NOT_PERMITTED** via the [DRC](02-artifacts/delegation-readiness-check/).

## What GTAF is not
GTAF is **not** an implementation guide, a tooling platform, or a certification scheme. It does not build or operate systems. It defines the **structural prerequisites** that must be true before delegation is allowed.

## Core artifacts (foundation)
- [System Boundary (SB)](02-artifacts/system-boundary/)
- [Decision Record (DR)](02-artifacts/decision-record/)
- [Responsibility Binding (RB)](02-artifacts/responsibility-binding/)
- [Delegation Readiness Check (DRC)](02-artifacts/delegation-readiness-check/)

## Lifecycle artifacts (operations)
- [Decision Review Board (DRB)](02-artifacts/decision-review-board/)
- [Emergency Intervention System (EIS)](02-artifacts/emergency-intervention-system/)
- [Decision Velocity Metrics (DVM)](02-artifacts/decision-velocity-metrics/)

## GTAF in one sentence
Delegation is allowed **only if** boundaries, authority, responsibility, and intervention are explicit, verifiable, and valid **within a defined scope and time window**.

## License & Citation
License: CC BY 4.0. Citation guidance: see [Citation & Versioning](00-meta/citation-and-versioning/).

## Quick Start (Minimal)
If you only do three things:

1. Define a **System Boundary (SB)** and scope it.  
2. Define **Decision Records (DR)** and bind outcome ownership with **RB**.  
3. Issue a **DRC** and allow delegation only if **PERMITTED**.

Start here:

- [Core Model Overview](01-core-model/overview/)
- [Minimal Application Path](06-application/minimal-application-path/)
- [Claims & Conformance](01-core-model/claims-and-conformance/)
