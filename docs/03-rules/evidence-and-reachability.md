# Evidence & Reachability Rules

## Purpose
This section defines what GTAF means by **evidence** and by **reachability** of escalation and intervention mechanisms. GTAF is implementation‑independent, but it is not reality‑independent: if an escalation path or kill‑switch is “defined” yet cannot be activated under real conditions, delegation is structurally unsafe.

Therefore, GTAF requires evidence references that make claims verifiable without prescribing tools, vendors, or operational delivery.

## Scope
This page specifies:

- the evidence model (what evidence is in GTAF and how it is referenced)
- the definition of reachability (escalation and intervention)
- minimal evidence sets by risk class
- DRC validation rules related to evidence and reachability
- failure modes and non‑compliant evidence patterns

Not in scope:

- implementation instructions (how to build escalations, how to implement kill‑switches)
- audit packaging formats (only reference‑grade evidence linking)

## Normative principles (binding)
- **E1 — Evidence is referenced, not delivered:** GTAF requires evidence as structured pointers; evidence is part of the structural claim.
- **E2 — Reachability is a safety property:** a path is valid only if it is reachable under realistic stress conditions.
- **E3 — Evidence must be minimally sufficient, not exhaustive:** minimum evidence needed to make a claim verifiable.
- **E4 — Evidence is scope‑bound and time‑bound:** evidence must be valid within the same scope and validity window as the artifacts it supports.
- **E5 — Absence of evidence is a blocker:** if required evidence is missing, DRC MUST be NOT_PERMITTED.

## Evidence model (normative)
**Evidence definition**
Evidence is any referenceable object that substantiates a structural claim, such as:

- policy or charter reference (mandate sources)
- runbook / procedure reference (escalation/intervention)
- access/permission attestations
- test results (reachability tests, drills)
- incident records showing mechanism activation
- architecture diagrams explicitly mapped to SB boundaries

**Evidence reference fields (recommended schema)**
Artifacts SHOULD reference evidence via a structured list such as:

- `evidence.id`
- `evidence.type` (MANDATE | PROCEDURE | ACCESS | TEST | LOG | DIAGRAM | INCIDENT | ATTESTATION)
- `evidence.title`
- `evidence.ref` (URL, doc id, repository path, ticket id — tool‑agnostic)
- `evidence.scope_ref` (optional)
- `evidence.valid_from`, `evidence.valid_until` (or review cycle)
- `evidence.owner.role`
- `evidence.integrity` (optional checksum/version tag)

**Normative rule:** evidence must be referenceable and stable enough that an independent reviewer can locate it and confirm it has not been replaced silently.

## Reachability (normative definition)
### 1) Escalation reachability
An escalation path is **reachable** if, when escalation conditions trigger, the responsible role(s) can be contacted and can assume control within the required **time‑to‑harm** window.

Reachability must consider:

- availability of responsible roles (coverage model)
- means of contact (channels)
- authority to intervene (permissions/mandate)
- environment conditions (partial outage, restricted access)

**Normative statement:** an escalation path is valid only if it can be activated in practice under degraded conditions within the time‑to‑harm constraints of the scope’s risk class.

### 2) Intervention reachability (kill-switch reachability)
An intervention mechanism (EIS) is **reachable** if the authorized role can trigger it:

- with realistic access constraints,
- within the required response time,
- without depending on the failing subsystem itself (where applicable).

**Normative statement:** a kill‑switch is structurally valid only if it remains callable when the delegated system is malfunctioning, compromised, or partially unavailable.

### Time-to-harm coupling (critical rule)
Reachability requirements are coupled to time‑to‑harm. If time‑to‑harm is short, reachability must be stronger and validated more frequently.

## Minimal evidence sets by risk class (normative baseline)
### Class A - Minimal evidence set
Required evidence references:

- mandate evidence for DR authority (e.g., charter ref)
- escalation evidence: where escalation is defined and who owns it

Recommended:

- basic reachability check record (test/drill), event‑based

### Class B - Expanded evidence set
Required:

- mandate evidence for DR + RB
- escalation procedure reference (who/when/how)
- escalation reachability verification (test record) with defined cadence
- intervention evidence if EIS is required by time‑to‑harm or scope design

Recommended:

- basic DVM baseline evidence (definition + reporting cadence)

### Class C - Mission-critical evidence set
Required (non‑negotiable):

- mandate evidence for DR and RB (traceable to formal authority)
- escalation procedure with coverage assumptions and time‑to‑harm linkage
- reachability test evidence (regular drills, at least monthly or event‑based with strict triggers)
- EIS procedure + activation authority evidence
- EIS reachability evidence showing it works under degraded conditions
- DVM baseline evidence and threshold‑to‑action mapping
- DRB review records as evidence of ongoing governance

## DRC evidence rules (normative)
A DRC can be PERMITTED only if:

- all required artifacts exist and are ACTIVE
- all required evidence references exist, are accessible, and are within validity window
- reachability claims are supported by test evidence when required by risk class

## Structured blockers (recommended)
- MISSING_EVIDENCE: escalation_procedure
- EVIDENCE_EXPIRED: kill_switch_drill
- REACHABILITY_NOT_VERIFIED: escalation
- EVIDENCE_NOT_ACCESSIBLE: mandate_ref
- EIS_DEPENDS_ON_FAILING_SYSTEM

## Reachability testing (tool-agnostic, normatively constrained)
**What must be proven (not how)**
Evidence must demonstrate:

- activation time measured vs allowed window
- authority: activating role actually had permissions
- independence: intervention does not depend on the compromised system
- traceability: test record exists and is immutable enough to trust

**Acceptable evidence formats (examples)**
- tabletop exercise record (only acceptable for Class A and some Class B contexts)
- drill report with timestamps and participants
- ticket/log showing real activation
- signed attestation (only acceptable if backed by periodic drills for Class C)

**Normative rule:** for Class C, tabletop‑only evidence is insufficient. A practical activation must be demonstrated.

## Integrity & anti-pattern rules (normative)
**Evidence anti‑patterns (invalid)**
- “Evidence” that is a dead link or inaccessible to accountable roles
- unverifiable claims without reference
- kill‑switch that requires access to the failing system to trigger
- escalation path that depends on a single unavailable person (no coverage model)
- evidence that is permanently “valid” with no review cycle in medium/high risk scopes

**Evidence integrity expectations**
Evidence should be stable and resistant to silent change:

- versioned documents where possible
- revision history or immutable logs
- clear ownership and review cadence

## Practical template (optional)
A simple “Reachability Evidence Record” can be used as a reusable evidence object:

- scope
- mechanism (escalation / EIS)
- tested scenario (normal / partial outage / compromised system)
- time‑to‑activate (measured)
- authority verification (who had access)
- outcome (pass/fail)
- next due date
