# Versioning & Change Control

## Purpose
This page defines how GTAF remains a **stable, licensable reference** over time while still evolving. Versioning and change control ensure that:

- artifact meaning is interpretable relative to a GTAF reference version,
- “GTAF conformity” is a time‑ and scope‑bound claim, not a vague statement,
- structural rules (invariants) remain enforceable without turning into consulting‑heavy negotiation.

Versioning in GTAF is not primarily about software release mechanics; it is about **preserving normative meaning**.

## Scope
This section specifies:

- GTAF reference versions and their semantics,
- artifact revisions vs reference versions,
- breaking vs non‑breaking changes,
- deprecation policy and lifecycle states,
- migration rules (how artifacts move across reference versions),
- change authority (who may decide what changes),
- event‑based revalidation triggers (when changes invalidate readiness).

Not in scope:

- tool‑specific workflows (Git, Jira, pipelines),
- certification programs or external audit formats.

## Core concepts (normative)
### V1 - Two-layer versioning: Reference vs Implementation
GTAF uses two distinct version layers that must never be confused:

1. **GTAF Reference Version** (`gtaf_ref.version`): the global, normative definition of artifact types, required fields, invariants, and interpretation rules.

2. **Implementation-layer lifecycle** (artifact revisions + validity windows): the local evolution of concrete SB/DR/RB/DRC/EIS/DRB/DVM artifacts within a scope, tracked via `revision` and bounded by `valid_from` / `valid_until` (or review cycle).

**Normative rule:** every artifact MUST bind to a GTAF reference version. Artifacts without `gtaf_ref.version` are structurally uninterpretable and cannot support readiness.

**Practical implication:** a scope may be fully up-to-date on its artifacts (ACTIVE, within validity) and still be **non-conformant** if it does not declare the correct GTAF reference version.

**Example (minimal):**
- A team operates with ACTIVE SB/DR/RB/DRC within valid windows, but `gtaf_ref.version` is missing → **NOT_CONFORMANT**.
- The same artifacts declare `gtaf_ref.version = GTAF-0.1` and are within validity → **potentially CONFORMANT** (subject to risk-class rules and evidence).

## GTAF reference version semantics (normative)
**Reference version format**
- `GTAF-MAJOR.MINOR` (e.g., `GTAF-0.1`, `GTAF-0.2`)
- optional pre‑release: `GTAF-0.1-rc1` (internal staging only)

**Meaning of version increments**
- **MAJOR**: breaking normative change (can invalidate artifact sets or change interpretation rules)
- **MINOR**: additive or clarifying change (new optional fields, new optional artifact types, clarifications)
- **PATCH** (optional): editorial fixes only (non‑semantic)

**Normative rule:** any change that alters a required field set, an invariant, or the interpretation of an existing field is a **MAJOR** change.

## Artifact lifecycle states (normative)
Artifacts MUST use the lifecycle states defined in the global schema:

- `DRAFT`: exists but not claimable for readiness
- `ACTIVE`: valid and claimable (within validity window)
- `DEPRECATED`: still valid but scheduled for replacement/removal; must have a successor plan
- `RETIRED`: no longer valid; kept for traceability only

**Deprecation requirements (normative)**
If an artifact becomes `DEPRECATED`, it MUST contain:

- `deprecation.reason`
- `deprecation.successor_ref` (new artifact ID or planned replacement)
- `deprecation.sunset_date` (after which it becomes `RETIRED`)

## Change classes (breaking vs non-breaking)
**Non‑breaking changes (allowed under MINOR)**
- adding optional fields
- introducing a new lifecycle artifact not required for existing A/B scopes
- clarifying text/definitions/examples without changing invariants
- adding additional DVM metric definitions without making them mandatory for existing classes

**Breaking changes (require MAJOR)**
- introducing a new required field for SB/DR/RB/DRC
- changing the meaning of an enum value
- tightening an invariant (e.g., making EIS mandatory for Class B)
- changing what “PERMITTED” means in DRC logic
- changing scope taxonomy in a way that reinterprets existing claims

**Normative rule:** a breaking change MUST include an explicit migration path.

## Authority & governance of changes (normative)
Changes to the GTAF reference are decided by a designated authority (e.g., “GTAF Reference Stewardship”).

Minimum requirements:

- `reference_change.authority_role` exists
- change proposals are recorded as structured **Reference Change Records (RCR)**

### Reference Change Record (RCR) (recommended)
RCR is the canonical change log entry for the GTAF reference. It SHOULD include:

- `RCR-ID`
- affected reference version target
- change type: breaking / non‑breaking
- rationale
- impacted artifacts/invariants
- migration notes
- adoption timeline

This keeps reference evolution auditable without turning into a training/consulting product.

## Migration & compatibility (normative)
**Compatibility modes**

1. **Strict compatibility (preferred):** artifacts created under reference version X remain interpretable under X.

2. **Declared migration:** artifacts are formally migrated to reference version Y via controlled steps.

**Normative rule:** “GTAF conformity” claims MUST specify the reference version they refer to. A claim without version is invalid.

**Migration requirements**
When migrating a scope from reference X → Y, the migration MUST:

- list all impacted artifact types
- identify any missing required fields introduced by Y
- update invariants and re‑run readiness validation (DRC)

**Migration result is a new state**
Migration is not a silent reinterpretation. It yields:

- new artifact revisions (same IDs) or successor artifacts (new IDs)
- updated `gtaf_ref.version`
- updated `change_reason`
- new DRC issuance for any semi/autonomous contexts

## Event-based revalidation triggers (normative)
Even without a reference version change, the following events MUST trigger review and may invalidate readiness:

**Triggers related to boundaries (SB)**
- boundary changes (included/excluded components)
- interface changes (new allowed interfaces, increased access)
- legal/org mapping changes (ownership shifts, outsourcing, mergers)

**Triggers related to decision spaces (DR)**
- changes to allowed actions or impact limits
- delegation level changes
- new triggers or altered escalation paths
- expiry policy changes

**Triggers related to responsibility (RB)**
- role changes (outcome owner, escalation owner)
- mandate changes (board/charter updates)
- handover events without explicitly preserved accountability

**Triggers related to operation (DRB/EIS/DVM)**
- changes to review frequency in medium/high risk scopes
- changes to kill‑switch authority or reachability assumptions
- threshold changes that affect when intervention is required

**Normative rule:** any trigger event in a scope containing autonomous or semi‑autonomous delegation MUST cause DRC to be reissued (or explicitly invalidated).

## Validity windows vs version changes (normative)
Validity windows apply at artifact level (SB/DR/RB/DRC…) and are independent from reference version changes. However:

- a reference **MAJOR** change SHOULD force review of all ACTIVE artifacts in the affected scope,
- a scope may run multiple reference versions across different scopes, but within a single scope, mixed versions SHOULD be avoided unless explicitly justified.

## Claim format: GTAF conformity statement (normative)
Any statement of conformity MUST be expressible as:

`Conformity Claim = (Scope, GTAF Reference Version, Time Window, Evidence References)`

Minimum claim fields:

- `scope.id`
- `gtaf_ref.version`
- `valid_from`, `valid_until`
- `claim.basis`: list of relevant DRC IDs (or a DRC set)
- optional: risk class

Without these fields, the claim is structurally undefined and must be treated as **marketing, not reference validity**.

## Deprecation strategy (practical, normative intent)
**When to deprecate**
- an artifact is superseded by a clearer boundary/decision structure
- a mandate model changed
- a scope split/merge requires new IDs or successor structures

**What deprecation prevents**
Deprecation prevents “silent drift”: old assumptions remain referenced long after reality changed.

## Guardrails
- Versioning must not become a consulting product. The reference must remain self‑contained.
- Change control must not become bureaucratic theater; it preserves normative meaning.
- Avoid “implicit upgrades.” If interpretation changes, it is a **MAJOR** change.
