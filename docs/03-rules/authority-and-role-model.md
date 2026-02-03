# Authority & Role Model (Minimum Viable Governance)

## Purpose
This page defines the minimum viable authority and role model required for GTAF to function as a normative framework. GTAF is role‑based by design: decisions, responsibilities, escalation paths, and interventions must be anchored in **roles and mandates**, not persons.

Without an explicit authority model, GTAF collapses into informal power (“whoever can act”) and becomes negotiable.

The goal is to define the smallest, consistent set of roles and authority bindings that makes:

- artifact issuance legitimate,
- escalation and intervention actionable,
- accountability continuous across handovers,
- conformity claims meaningful.

## Scope
This section specifies:

- canonical GTAF roles (minimum set)
- authority rights per artifact type (who may create/approve/activate)
- mandate anchoring requirements
- scope‑binding rules for authority (Authority‑to‑Scope)
- separation of duties (SoD) for medium/high risk contexts
- handover continuity rules (role transitions)

Not in scope:

- HR job descriptions or org chart design
- implementation of access management (IAM) tooling
- staffing models, on‑call schedules (only the structural requirement for coverage)

## Normative principles (binding)
- **A1 — Roles, not persons:** artifacts MUST bind to roles. “Alice approved” is not valid; “CISO role approved under mandate X” is valid.
- **A2 — Authority is mandate‑bound:** any authority to issue or approve artifacts MUST reference a mandate source (charter, board resolution, contract).
- **A3 — Authority is scope‑bound:** authority is valid only within a defined scope. Global authority must be explicitly declared; otherwise authority is local.
- **A4 — Outcome ownership is non‑delegable:** execution may be delegated; outcome ownership (RB) cannot.
- **A5 — Intervention must remain reachable:** authority to activate emergency intervention must be explicitly defined and remain actionable under stress.
- **A6 — Separation of duties increases with risk:** avoid single‑point governance failures as risk class rises.

## Canonical role set (minimum viable)
You may rename roles per organization. The canonical set defines functional responsibilities, not titles.

1) **Scope Owner (SO)**
- Function: accountable owner of a scope (system domain / decision domain / org unit).
- Responsibilities: ensure scope definition exists and remains accurate; ensure artifact closure and revalidation triggers are handled.
- Typical mapping: Head of Platform, Head of Ops, Domain Lead.

2) **Decision Authority (DA)**
- Function: legitimate authority to define/approve DRs within a scope.
- Binding: must reference mandate source.
- Typical mapping: CTO/CISO/Executive delegate (domain‑dependent).

3) **Outcome Owner (OO)**
- Function: role that carries outcome accountability for the decision space (RB binding).
- Key property: cannot be a system.
- Typical mapping: Product Owner, Head of Operations, Service Owner.

4) **Escalation Owner (EO)**
- Function: owns escalations and ensures escalation reachability (coverage/procedure).
- Typical mapping: Head of Ops / Incident Commander role / Security Officer role.

5) **Intervention Authority (IA)**
- Function: role authorized to activate EIS/kill‑switch for a scope/boundary/target.
- Typical mapping: CISO / Head of Ops / delegated executive authority.
- Class C: IA MUST be explicit and typically dual‑authorized or independently reviewable.

6) **Review Authority (RA) / DRB Chair**
- Function: owns the DRB regime; ensures drift review and outputs occur.
- Typical mapping: Governance lead, Security governance, Architecture governance.

7) **Reference Steward (RS)** (GTAF internal)
- Function: maintains GTAF reference version, schemas, and change control records (RCR).
- Note: usually inside GTAF stewarding org or customer governance function.

## Authority matrix (normative)
This matrix defines who has authority to issue / approve / activate each artifact type. Approval authority MUST be defined.

**System Boundary (SB)**
- Propose/Draft: SO
- Approve/Activate: DA or designated Architecture Authority (if defined)
- Required mandate: recommended (mandatory for B/C)

**Decision Record (DR)**
- Draft: SO or delegated authors
- Approve/Activate: DA (mandatory)
- Required mandate: mandatory (all classes)

**Responsibility Binding (RB)**
- Draft: SO
- Approve/Activate: OO **and** mandate‑bearing authority (DA or executive mandate source)
- Required mandate: mandatory (all classes)
- Normative constraint: RB must not be self‑assigned without mandate.

**Delegation Readiness Check (DRC)**
- Evaluate/Issue: SO or delegated governance function
- Approve (if required):

  - Class A: optional
  - Class B: RA recommended
  - Class C: RA mandatory
- Normative constraint: DRC is derived; approval acknowledges the derived result, not overrides it.

**Decision Review Board (DRB)**
- Define: RA
- Approve/Activate: DA or governance charter (org‑dependent)
- Required mandate: mandatory in B/C scopes

**Emergency Intervention / Kill‑Switch (EIS)**
- Define: IA + SO recommended
- Approve/Activate: IA (mandatory)
- Required mandate: mandatory in C, conditional in B

**Decision Velocity Metrics (DVM)**
- Define: RA or SO
- Approve: RA recommended; mandatory in C
- Required mandate: recommended (mandatory in C if tied to intervention thresholds)

## Authority-to-Scope binding (normative)
- **AS1 — Authority must declare scope coverage:** every DA/IA/RA MUST be bound to which scope(s) it covers (scope.id list or pattern) and a validity window/review cycle.
- **AS2 — No implicit cross‑scope authority:** authority in one scope does not extend to another unless explicitly bound by mandate.
- **AS3 — Multi‑boundary scopes require explicit authority resolution:** if a DECISION_DOMAIN spans multiple SBs, authority must specify whether DA is global across all SBs or per‑SB (preferred for high risk).

## Separation of duties (SoD) (risk-adjusted)
**Class A (Low risk)**
- DA may also be RA if scope is small, but escalation must remain independent.

**Class B (Medium risk)**
- RA should be distinct from DA (recommended)
- IA should not be the same as OO (recommended)

**Class C (High / mission critical)**
Minimum SoD constraints (normative defaults):

- DA and RA MUST be distinct roles
- IA MUST not be the same as the primary OO
- DRB Chair (RA) must not be the same as the authority that unilaterally benefits from delegation outcomes

If an org cannot satisfy SoD for Class C, delegation should be NOT_PERMITTED by governance insufficiency.

## Handover & continuity rules (normative)
**H1 — Role transition requires explicit continuity**
If an accountable role changes (OO/EO/IA/DA), one of the following MUST occur:

- update RB/DR with new role binding and mandate continuity, and/or
- issue new DRC (mandatory for semi/autonomous contexts)

**H2 — No “gap accountability”**
There must never be a period where:

- a DR remains active but RB has no valid outcome owner, or
- an EIS exists but no active IA role can activate it.

If such a gap occurs, DRC MUST be NOT_PERMITTED.

**H3 — Coverage is required where time‑to‑harm is short**
For B/C contexts, escalation/intervention roles must have an explicit coverage model (can be referenced as evidence).

## Minimal “authority graph” (practical representation)
You can represent authority bindings as a simple graph (tool‑agnostic):

- Scope → {SO}
- Scope → {DA, RA, IA} (with mandate refs)
- DR → DA
- RB → OO + mandate
- Escalation Path → EO
- EIS → IA
- DRB → RA

This graph prevents “hidden governance”.

## Anti-patterns (non-compliant)
- Authority defined by person names instead of roles
- RB assigned without mandate source
- Same role authors DR, binds RB, issues DRC, chairs DRB, and is IA in Class C
- EIS authority unclear or depends on the failing system’s administrators
- Scope owner is undefined; artifacts float without accountability
