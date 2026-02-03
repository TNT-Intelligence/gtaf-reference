# Glossary

## Purpose
This glossary defines **normative GTAF terminology**. Terms in GTAF are not stylistic; they determine meaning, validity, and what can be claimed. If a term is used inconsistently, the framework becomes negotiable and loses its function.

Normative rule: When a term is defined here, artifact schemas and specs must use the term consistently. Local synonyms may exist for readability, but the canonical term must remain stable.

## Core Terms (Normative)

## Artifact
A structured, identifiable state description that constitutes normative reality in GTAF. Artifacts are not “documentation”; they are the authoritative representation of boundaries, mandates, decisions, readiness, and lifecycle controls.

Key properties: identity, scope binding, validity window, revision, references.

## Foundation Artifacts
The minimal set of artifacts required to define delegation and responsibility:

- [System Boundary (SB)](/02-artifacts/system-boundary/)
- [Decision Record (DR)](/02-artifacts/decision-record/)
- [Responsibility Binding (RB)](/02-artifacts/responsibility-binding/)
- [Delegation Readiness Check (DRC)](/02-artifacts/delegation-readiness-check/)

## Lifecycle Artifacts
Artifacts that enable safe operation over time:

- [Decision Review Board (DRB)](/02-artifacts/decision-review-board/)
- [Emergency Intervention / Kill‑Switch (EIS)](/02-artifacts/emergency-intervention-system/)
- [Decision Velocity Metrics (DVM)](/02-artifacts/decision-velocity-metrics/)

## System Boundary (SB)
A formal definition of where responsibility and liability apply and stop, expressed as included/excluded components, allowed interfaces, data spaces, and mapping to organizational/legal ownership.

Normative implication: No delegation is valid without an [SB](/02-artifacts/system-boundary/).

## Decision Record (DR)
A formal representation of a delegable decision space: what can be decided, under which constraints, by whom (role), with which delegation level, triggers, escalation, and expiry policy.

Not: a meeting note, a rationale essay, or a process flow.

Related terms (non-binding, mapping): decision rights, decision policy.  
Origins: decision-rights governance literature (e.g., RAPID-style frameworks).

## Responsibility Binding (RB)
A formal binding that assigns outcome ownership for one or more DRs to a role and mandate source. RB ensures accountability remains human/organizational even when systems act autonomously.

Normative implication: No semi‑autonomous or autonomous delegation is valid without an [RB](/02-artifacts/responsibility-binding/).

Related terms (non-binding, mapping): accountability assignment, RACI owner.  
Origins: RACI-style responsibility assignment matrices.

## Delegation Readiness Check (DRC)
A binary validation artifact representing whether delegation for a specific target context is structurally PERMITTED or NOT_PERMITTED, based on completeness and validity of required artifacts and evidence.

Normative implication: [DRC](/02-artifacts/delegation-readiness-check/) is non‑negotiable; missing prerequisites yield NOT_PERMITTED.

Related terms (non-binding, mapping): readiness gate, governance gate.  
Origins: governance gating practices in safety and compliance programs.

## Delegation
The transfer of actionable decision space from a human role to a target (agent, workflow, system, or team). Delegation is allowed only when authority, boundary, responsibility, and intervention are explicit and verifiable.

## Delegation Level
Defines the autonomy degree of a delegated target:

- ASSISTIVE: suggests, humans decide
- SEMI_AUTONOMOUS: executes within strict constraints but requires structured oversight/escalation
- AUTONOMOUS: executes decisions within defined boundaries without prior human approval

Normative implication: higher delegation levels increase risk by default.

## Authority (Decision Authority)
The legitimate right to define or approve a decision space (DR) within a scope. Authority is role‑based and anchored in a mandate source.

Not: informal influence or de facto power.

## Mandate
The formal source that legitimizes authority and responsibility assignments (e.g., governance charter, board resolution, contract). Mandates are referenced and time‑bound.

## Outcome Ownership
The organizational responsibility for outcomes produced by a decision space, regardless of who/what executed it. Outcome ownership is bound via RB.

Key distinction: execution can be automated; outcome ownership cannot.

## Escalation Path
A defined, ordered route for human takeover when conditions exceed boundaries or anomalies occur. Escalation is valid only if it is reachable within time‑to‑harm constraints.

## Reachability
A safety property: the practical ability to activate escalation or intervention under realistic stress/degraded conditions within the required time window.

## Emergency Intervention / Kill-Switch (EIS)
A structural mechanism, defined as an artifact, that allows authorized roles to immediately suspend delegated authority for a scope, boundary, DR, or target.

Normative implication: mandatory for Class C and for scopes with short time‑to‑harm. See [EIS](/02-artifacts/emergency-intervention-system/).

Related terms (non-binding, mapping): kill switch, emergency stop.  
Origins: safety and operational control practices.

## Decision Review Board (DRB)
A defined review regime that periodically validates decision quality, detects drift, and triggers revalidation or suspension. DRB operates against artifacts and evidence.

Related terms (non-binding, mapping): governance review board, oversight board.  
Origins: governance review bodies in risk and compliance regimes.

## Decision Drift
Deviation over time between intended decision boundaries/behavior and observed outcomes or execution patterns, especially in autonomous or agentic systems. Drift is addressed by DRB and, where necessary, EIS.
Also called Agent Drift.

## Decision Debt
The accumulation of implicit, undocumented, or unbound decision‑making that increases operational fragility and erodes accountability.

Indicator: decisions are made/executed without DR/RB/DRC closure.

## Decision Velocity Metrics (DVM)
A metric set designed as an early warning system for structural decay (speed exceeding integrity). DVM is not a performance KPI but a governance signal.

Related terms (non-binding, mapping): governance health metrics, early warning indicators.  
Origins: risk and operational monitoring practices.

## Scope
A bounded applicability domain for GTAF meaning and validity. Every artifact and every conformity claim must be expressed within a scope.

Canonical scope kinds:

- LEGAL_ENTITY
- ORG_UNIT
- SYSTEM_DOMAIN
- DECISION_DOMAIN

## Scope Record
Structured record of a scope (id, kind, boundary anchor, ownership, risk class, validity, and change control references).

## Conformity (GTAF-Conformant)
A binary, scope‑bound claim that a set of artifacts and evidence satisfies GTAF structural prerequisites for delegation, relative to a GTAF reference version and within a validity window.

Not: a maturity score or generic quality label.

## Conformity Claim
Canonical statement of GTAF conformity: (Scope, GTAF Reference Version, Time Window, Evidence/DRC Basis).

## Reference Version
The versioned normative definition of artifact types, required fields, and invariants. Artifacts are interpretable only relative to a reference version.
Also called GTAF Reference.

## Reference Change Record (RCR)
Structured change log entry for GTAF reference evolution (change type, rationale, impacts, and migration notes).

## Artifact Revision
The evolution of a specific artifact instance over time while retaining identity (ID). Revisions capture change history and maintain traceability.

## Validity Window
The time span during which an artifact (or claim) is considered active and applicable. Validity requires review cycles and revalidation triggers.

## Evidence
Referenceable objects (documents, logs, test records, diagrams) that substantiate structural claims, especially mandates and reachability.

See: [Evidence & Reachability Rules](/03-rules/evidence-and-reachability/).

## Time-to-Harm
The maximum time window between a failure/anomaly and unacceptable harm. Time‑to‑harm determines required reachability and review rigor.

## Risk Class (A/B/C)
A normative classification used to set minimum structural requirements:

- A: low risk, reversible, bounded
- B: material impact, moderate exposure
- C: mission critical, irreversible/severe exposure

## Terminology Guardrails (Anti-Patterns)
The following uses are non‑compliant with GTAF language:

- “We are GTAF compliant” without scope/version/time window
- “DRC is YES because we trust the team” (belief ≠ validation)
- “Kill‑switch exists” without reachability evidence
- “Boundary is defined” without included/excluded and allowed interfaces
