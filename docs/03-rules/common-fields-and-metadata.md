# Common Fields and Metadata

## Required common fields
- `scope.id`, `scope.kind`, `scope.boundary_ref`
- `gtaf_ref.version`
- `status` (DRAFT | ACTIVE | DEPRECATED | RETIRED)
- `valid_from`, `valid_until` (or review cycle)
- `revision`

## Evidence model (normative)
Evidence is referenced, not delivered. It must be stable and accessible.

See: [Evidence & Reachability Rules](../03-rules/evidence-and-reachability/).

Recommended evidence fields:

- `evidence.id`
- `evidence.type` (MANDATE | PROCEDURE | TEST | LOG | DIAGRAM | INCIDENT | ATTESTATION)
- `evidence.ref` (tool‑agnostic pointer)
- `evidence.valid_from`, `evidence.valid_until`
- `evidence.owner.role`

### Minimal evidence by risk class
- **Class A**: mandate + escalation procedure references
- **Class B**: mandate for DR/RB + escalation procedure + reachability test evidence
- **Class C**: mandate + escalation coverage + EIS procedure + EIS reachability drills + DRB records + DVM baseline

## Reachability
Reachability is a safety property: escalation/intervention must be practically reachable within [time‑to‑harm](../10-terminology/glossary/#time-to-harm) constraints.

## Authority model (minimum viable)
Artifacts bind to roles, not persons. Authority MUST reference a mandate source and scope coverage.

Canonical roles:

- Scope Owner (SO)
- Decision Authority (DA)
- Outcome Owner (OO)
- Escalation Owner (EO)
- Intervention Authority (IA)
- Review Authority (RA)

See: [Authority & Role Model](../03-rules/authority-and-role-model/).

## Separation of duties (risk-adjusted)
- Class A: DA and RA may be same role in small scopes
- Class B: DA and RA should be distinct
- Class C: DA and RA MUST be distinct; IA must not be the primary OO

## Handover rules
Role transitions MUST preserve accountability. Gaps in ownership invalidate readiness.
