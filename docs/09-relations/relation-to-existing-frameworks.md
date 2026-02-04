# Related Work / Theoretical Anchor

## Purpose
This page positions GTAF relative to existing standards, frameworks, and research. GTAF is not intended to replace established governance or security frameworks; it introduces a **missing formal layer**: delegation semantics (who may delegate what to which target under which boundaries, with which human outcome ownership, under what intervention reachability, and under which validity window).

Primary functions:

1. prevent GTAF from becoming self‑referential,

2. ensure terminological and conceptual compatibility where appropriate,

3. define precisely where GTAF is different and why it exists.

**Normative guardrail:** this page is contextual. It must not redefine GTAF terms or artifact invariants. If a conflict arises between related‑work terminology and the GTAF glossary, the GTAF glossary governs.

## How GTAF relates to existing work
GTAF typically relates to other frameworks in one of three ways:

1. **Complement (adds a missing layer):** GTAF adds structural delegation permissioning (SB/DR/RB/DRC + lifecycle semantics).

2. **Attach (provides concrete formalization):** where other frameworks specify governance intentions, GTAF provides artifact‑level formalization that makes those intentions auditable and non‑negotiable.

3. **Integrate (bridges into technical boundaries):** where technical frameworks control access or infrastructure quality, GTAF defines decision authority, ownership, and liability boundaries upstream.

## Standards & governance frameworks
### ISO/IEC 42001 (AI Management System)
**What it is:** defines requirements for establishing, implementing, maintaining, and continually improving an AI management system (AIMS).

**Overlap:** governance, risk management, lifecycle thinking, accountability structures.

**Where GTAF differs (core):** ISO 42001 is a management‑system standard; it does not prescribe GTAF’s delegation gate semantics (DRC as a binary permission artifact derived from closure + evidence + reachability). GTAF can operationalize parts of AIMS without claiming to be ISO 42001.

### NIST AI RMF 1.0
**What it is:** voluntary guidance to manage AI risks across functions (GOVERN, MAP, MEASURE, MANAGE).

**Overlap:** governance and risk framing; accountability emphasis.

**Where GTAF differs (core):** AI RMF is intentionally not a checklist and is not a permissioning mechanism; GTAF introduces a binary **structural permission to delegate** (DRC) with formal artifact closure for specific delegation contexts.

### EU AI Act (post-market monitoring for high-risk systems)
**What it is:** requires post‑market monitoring systems for high‑risk AI systems proportionate to risks.

**Overlap:** lifecycle control, monitoring obligations, evidence expectations over time.

**Where GTAF differs (core):** regulatory vs structural. GTAF provides operationally tractable structures such as DRB (review regime), DVM (early‑warning signals), and EIS (explicit intervention authority for short time‑to‑harm contexts) without claiming regulatory compliance by itself.

### ISO/IEC 27001 (ISMS) and TISAX
**What they are:** ISO/IEC 27001 defines ISMS requirements. TISAX is an assessment and exchange mechanism widely used in the automotive supply chain.

**Overlap:** governance, control objectives, audit readiness, evidence discipline.

**Where GTAF differs (core):** these focus on security controls and assessment mechanisms; GTAF focuses on decision authority and responsibility binding as prerequisites for safe delegation—especially when automation increases decision velocity beyond organizational integrity.

## Security & architecture frameworks
### Zero Trust Architecture (NIST SP 800-207)
**What it is:** shifts defenses from static perimeters toward users/assets/resources and continuous verification.

**Overlap:** boundary concepts and enforcement posture.

**Where GTAF differs (core):** Zero Trust addresses connection and access trust; GTAF addresses **decision trust**: who is authorized to define delegable decision spaces, what is inside/outside a boundary, and who remains outcome owner even when execution is automated.

### AWS Well-Architected Framework
**What it is:** evaluates architectures across pillars such as operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability.

**Overlap:** architectural review discipline; “questions to ask” mentality.

**Where GTAF differs (core):** Well‑Architected is about system quality attributes; GTAF focuses on authority, responsibility, and delegation structure. GTAF operates upstream to define who may decide architecture tradeoffs and within which mandated boundaries.

## Decision rights & organizational frameworks
### RAPID (Bain)
**What it is:** assigns decision roles (Recommend, Agree, Perform, Input, Decide).

**Overlap:** role clarity in decision‑making.

**Where GTAF differs (core):** RAPID clarifies decision roles but does not bind them to technical boundaries, delegation levels, reachability, or a binary readiness gate. GTAF can be seen as “RAPID made delegation‑safe” by binding decision rights to SB/DR/RB and validating readiness via DRC.

## A compact decision test (talks)
If a framework answers mainly:

- “How do we manage risk/governance?” → ISO 42001, NIST AI RMF
- “How do we secure access?” → Zero Trust, OPA
- “How do we design robust architectures?” → Well‑Architected
- “Who plays what role in a decision?” → RAPID

…then GTAF answers:

- “Is this delegation structurally permitted—here, now, for this scope—given authority, boundaries, ownership, intervention reachability, and validity?”

## Theoretical anchors (academic)
For academic foundations, see [Academic Context](../09-relations/academic-context/).

## Practical implication: compatibility, not replacement
- ISO/IEC 42001 / NIST AI RMF / EU AI Act define governance goals and obligations.
- Zero Trust / Well‑Architected support secure and robust system design.
- RAPID clarifies roles in decisions.
- GTAF defines whether delegation is **structurally permitted**, and makes that permission claimable only within scope/version/time‑window semantics.

See also: [Comparison Lens](../09-relations/comparison-lens/).

## Suggested reference list (starter set)
This is a short, curated bibliography (non‑exhaustive):

- ISO/IEC 42001 standard overview
- NIST AI RMF 1.0 (AI 100‑1)
- EU AI Act Article 72 (post‑market monitoring)
- NIST SP 800‑207 Zero Trust Architecture
- AWS Well‑Architected pillars
- Bain RAPID decision roles
- Jensen & Meckling (1976) agency costs
- Matthias (2004) responsibility gap
- Weick (Sensemaking in Organizations)
- STPA/STAMP tutorial/handbook

## Guardrails (avoid misrepresentation)
- Do not claim “ISO 42001 compliant” or “AI Act compliant” unless a dedicated conformity assessment exists. References are contextual anchors, not certifications by default.
- Avoid copying normative text from standards; prefer paraphrase and citation.
