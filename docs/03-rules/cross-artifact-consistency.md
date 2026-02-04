# Cross-Artifact Consistency

## Referential closure
All referenced artifacts must exist and be valid within scope and validity window. Missing references are blockers.

## Scope coherence
Artifacts in a context must be within the same [scope](../10-terminology/glossary/#scope) or explicitly linked by cross‑scope rules. Scope leakage invalidates readiness.

## Conflict rules (normative)
- Conflicting DR boundaries without precedence => NOT_PERMITTED.
- Conflicting RB ownership without resolution => NOT_PERMITTED.
- Undefined scope precedence => NOT_PERMITTED.

## Minimal completeness checks
- Every SB has explicit included/excluded components and allowed interfaces.
- Every delegable DR has boundary, triggers, escalation, and expiry policy.
- Every semi‑autonomous DR has a binding RB.
- Every active delegation has a valid DRC.
- B/C scopes define DRB/EIS/DVM where required.
