# Invariants

These rules define **non‑negotiable validity**. If any invariant is violated, the state is structurally invalid and delegation must not be permitted.

## Core invariants (normative)

1. **Boundary invariant**: No delegation without a [System Boundary (SB)](../02-artifacts/system-boundary/).

2. **Decision invariant**: No delegable execution without a [Decision Record (DR)](../02-artifacts/decision-record/).

3. **Responsibility invariant**: No semi‑autonomous or autonomous execution without an active [Responsibility Binding (RB)](../02-artifacts/responsibility-binding/).

4. **Readiness invariant**: No activation without [DRC](../02-artifacts/delegation-readiness-check/) = PERMITTED.

5. **Temporality invariant**: Artifacts have [validity windows](../10-terminology/glossary/#validity-window) and must be within them.

6. **Non‑negotiability**: GTAF rules must not be softened; otherwise boundaries become political negotiation and lose function.