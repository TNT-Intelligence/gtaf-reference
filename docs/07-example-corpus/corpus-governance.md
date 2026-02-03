# Corpus Governance

The **Example Corpus** is a canonical, internally coherent set of GTAF artifact instances that demonstrate application **without becoming a template library**.

## Purpose

1. **Comprehension without training**: readers understand GTAF by seeing a complete, consistent set.

2. **Reference validity**: anchor cases stabilize interpretation across versions.

3. **Depth calibration**: show what “minimum sufficient” looks like for Class A/B/C.

The corpus is **not** a best‑practice catalog and **not** a certification baseline. It is a normative teaching object.

## Scope
This page specifies:

- structure and governance of the corpus
- selection rules for reference cases
- two canonical case sets (one lower‑risk, one higher‑risk)
- what completeness means for a case set (artifact closure)
- how the corpus is versioned and maintained

Not in scope:

- technical implementation details (platforms, pipelines, access tooling)
- organization‑specific policies
- copy/paste operational runbooks

## Normative principles (binding)
- **CXP1 — Canonical, not exhaustive**: the corpus remains small enough to stay coherent.
- **CXP2 — Artifact closure required**: all referenced artifacts exist, are in‑scope, and valid within the case window.
- **CXP3 — Tool‑agnostic realism**: boundaries, mandates, and reachability are described; tools are not prescribed.
- **CXP4 — Version‑bound interpretation**: every case binds to a GTAF reference version; cases are migrated or superseded explicitly.

## Corpus structure (recommended)
Each reference case SHOULD contain:

- Case ID (e.g., `CASE-001`)
- Risk Class (A/B/C)
- Scope Record (kind + boundary anchor)
- SB (1+)
- DR set (decision family)
- RB set (bindings)
- DRC set (readiness gates)
- For Class B/C: DRB regime, EIS definition, DVM baseline
- Evidence map (minimal references proving mandates and reachability where required)
- Change triggers (events that force revalidation)
- Canonical conformity claim statement: `(Scope, GTAF Reference Version, Time Window, DRC basis)`

## Completeness definition (artifact closure)
A reference case is complete only if:

1. all referenced artifact IDs exist and are ACTIVE (within validity window)

2. scope and boundary anchoring are explicit

3. DRC basis exists and can evaluate to PERMITTED only if evidence and reachability requirements are satisfied

4. for Class C: DRB, EIS, DVM are present and linked

5. the case contains a canonical conformity claim statement

## Versioning and maintenance
- Each case binds to a reference version.
- If the reference evolves, the case is either migrated or superseded by a new case ID (old case deprecated).

## Corpus governance & maintenance (recommended, reference-grade)
**Corpus ownership**
- Corpus is owned by a designated role (e.g., Reference Steward).
- Updates require a Reference Change Record (RCR) when they change interpretation.

**Versioning**
- Each case set binds to a GTAF reference version.
- If the reference evolves, the case is either migrated (new revisions, same IDs) or superseded (new CASE ID; old case deprecated).

**Guardrails**
- Cases must not become templates for customers.
- Cases must not embed tool‑specific implementation details.
- Cases must remain coherent and small.