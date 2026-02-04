# Event Catalog (Normative Event Codes)

## Purpose
This catalog defines canonical event codes used across GTAF to reference lifecycle triggers consistently. Events are not “incidents” or “changes” in a vague sense; they are **normative transition triggers** for the Delegation Context State Machine.

Event codes allow:

- deterministic invalidation vs review‑required semantics,
- consistent [DRC](../02-artifacts/delegation-readiness-check.md) blocker attribution,
- traceable [DRB](../02-artifacts/decision-review-board.md) outputs (“why was delegation suspended?”),
- claim revocation/renewal reasons that are machine‑checkable without prescribing tooling.

**Normative rule:** if an event appears in this catalog, it MUST be referenced by its code in DRC blockers, DRB outputs, and claim lifecycle notes (where applicable). If an event is used operationally but not cataloged, it must be added via change control.

## Scope
This page specifies:

- event code format and required fields
- event categories
- each canonical event definition
- normative transition effects (invalidate, suspend, review)
- minimum required artifact actions per event

Not in scope:

- technical monitoring, alerting, or ticket workflows
- incident postmortems (only the structural trigger semantics)

## Event code format (normative)
Code format: `E-<CATEGORY><NUMBER>`

Examples:

- `E-A1` (Definition event)
- `E-D3` (Deterministic invalidation due to delegation change)
- `E-E2` (Emergency incident stop)

## Required event fields (normative)
Each event definition MUST specify:

- Trigger (what happened)
- Applies to (scope/boundary/DR/target)
- Default transition (state machine)
- Effect semantics: INVALIDATE | SUSPEND | REVIEW_REQUIRED
- Required actions (minimum)
- Required artifacts affected (minimum set)
- Notes (optional clarifications)

## Effect semantics (normative)
**INVALIDATE**
- DRC becomes invalid immediately for the affected context(s)
- delegation must stop for semi/autonomous contexts
- transition target: INVALIDATED (or RECOVERY once remediation starts)

**SUSPEND**
- delegation must stop immediately
- [EIS](../02-artifacts/emergency-intervention-system.md) may be activated (mandatory in Class C if severe)
- transition target: SUSPENDED

**REVIEW_REQUIRED**
- does not automatically stop delegation if all validity windows remain intact
- requires DRB review (mandatory in B/C)
- may lead to INVALIDATE/SUSPEND based on review output

Normative default: in Class C, treat REVIEW_REQUIRED conservatively—often as SUSPEND unless explicitly justified.

## Categories
- **A — Definition/Construction** (scope and initial setup)
- **B — Evaluation/Issuance** (DRC/claim issuance)
- **C — Time/Validity** (expiry/renewal)
- **D — Change Events** (deterministic invalidation triggers)
- **E — Drift & Incident** (behavior deviation, emergency stop)
- **F — Reference Evolution** (GTAF reference version changes)

## Canonical events

### A) Definition / Construction Events
#### E-A1 - Scope anchored
- **Trigger:** scope record created with boundary anchor (SB)
- **Effect:** REVIEW_REQUIRED (enables drafting)
- **Transition:** UNDEFINED → DRAFTING
- **Required actions:** define scope.id/kind; link SB
- **Artifacts:** Scope Record, [SB](../02-artifacts/system-boundary.md) (anchor)

#### E-A2 - Artifact set drafted
- **Trigger:** initial SB/DR/RB drafted for a context
- **Effect:** REVIEW_REQUIRED
- **Transition:** DRAFTING → EVALUABLE (only if closure exists)
- **Required actions:** ensure closure and required fields
- **Artifacts:** SB, [DR](../02-artifacts/decision-record.md), (RB if needed)

### B) Evaluation / Issuance Events
#### E-B1 - DRC issued (PERMITTED)
- **Trigger:** DRC evaluation yields no blockers
- **Effect:** REVIEW_REQUIRED (informational)
- **Transition:** EVALUABLE → PERMITTED
- **Required actions:** record closure, evidence, window, result
- **Artifacts:** DRC (+ references)

#### E-B2 - DRC issued (NOT_PERMITTED)
- **Trigger:** DRC evaluation yields blockers
- **Effect:** INVALIDATE (for semi/autonomous contexts)
- **Transition:** remains EVALUABLE
- **Required actions:** record blockers; remediation plan
- **Artifacts:** DRC

#### E-B3 - Claim issued
- **Trigger:** conformity claim record created and published
- **Effect:** REVIEW_REQUIRED
- **Transition:** none (overlay)
- **Required actions:** link DRC basis and scope/version/window
- **Artifacts:** Claim record (if used)

### C) Time / Validity Events
#### E-C1 - Expiry approaching
- **Trigger:** DRC/claim/evidence within renewal threshold (policy‑defined)
- **Effect:** REVIEW_REQUIRED
- **Transition:** PERMITTED → EXPIRING
- **Required actions:** schedule renewal; DRB review in B/C
- **Artifacts:** DRC / Claim / Evidence refs

#### E-C2 - DRC expired
- **Trigger:** DRC valid_until reached
- **Effect:** INVALIDATE
- **Transition:** PERMITTED | EXPIRING → INVALIDATED
- **Required actions:** stop delegation; begin recovery; reissue DRC
- **Artifacts:** DRC (claim invalidated)

#### E-C3 - Claim expired
- **Trigger:** claim valid_until reached (even if DRC still valid)
- **Effect:** REVIEW_REQUIRED (operationally: claim no longer usable)
- **Transition:** none (DC may remain PERMITTED)
- **Required actions:** renew claim if used
- **Artifacts:** Claim record

#### E-C4 - Evidence expired
- **Trigger:** required evidence validity ends (mandate/procedure/drill)
- **Effect:** INVALIDATE (B/C mandatory; A if evidence required for that DC)
- **Transition:** PERMITTED | EXPIRING → INVALIDATED
- **Required actions:** renew evidence; re‑verify reachability if applicable
- **Artifacts:** Evidence refs, DRC

### D) Change Events (Deterministic Invalidation)
#### E-D1 - SB boundary expanded
- **Trigger:** SB included components expanded or excluded removed
- **Effect:** INVALIDATE
- **Transition:** PERMITTED | EXPIRING → INVALIDATED
- **Required actions:** reassess risk; update DR boundaries; reissue DRC
- **Artifacts:** SB, DR, DRC (and possibly RB)

#### E-D2 - SB interface widened
- **Trigger:** new allowed interface, broader data access, new integration
- **Effect:** INVALIDATE
- **Required actions:** update SB; verify enforcement expectations; reissue DRC
- **Artifacts:** SB, DRC (+ evidence if reachability assumptions change)

#### E-D3 - DR boundary changed
- **Trigger:** allowed actions / impact limits / triggers / exclusions changed
- **Effect:** INVALIDATE
- **Required actions:** amend DR; verify RB; reissue DRC
- **Artifacts:** DR, RB (if needed), DRC

#### E-D4 - Delegation level increased
- **Trigger:** assistive → semi/autonomous, or tighter autonomy removed
- **Effect:** INVALIDATE
- **Required actions:** reclassify risk; ensure RB/DRB/EIS/DVM requirements; reissue DRC
- **Artifacts:** DR, RB, DRB/EIS/DVM (if required), DRC

#### E-D5 - Authority / mandate changed
- **Trigger:** DA/OO/IA/EO role binding or mandate source changed
- **Effect:** INVALIDATE
- **Required actions:** update DR/RB/EIS; ensure continuity; reissue DRC
- **Artifacts:** DR, RB, EIS (if affected), DRC, Evidence refs

#### E-D6 - Scope changed
- **Trigger:** scope split/merge; boundary anchor changes; precedence rules changed
- **Effect:** INVALIDATE
- **Required actions:** update scope model; resolve overlaps; reissue relevant DRCs
- **Artifacts:** Scope Record, SB, DRC(s)

#### E-D7 - Conflict introduced (ambiguity)
- **Trigger:** overlapping DRs, conflicting RB ownership, undefined precedence
- **Effect:** INVALIDATE
- **Required actions:** resolve conflict; define precedence; reissue DRC
- **Artifacts:** DR/RB/Scope precedence, DRC

### E) Drift & Incident Events
#### E-E1 - Drift suspected (signal)
- **Trigger:** DVM threshold breach or DRB drift signal
- **Effect:** REVIEW_REQUIRED (Class B) / SUSPEND default (Class C)
- **Required actions:** DRB convenes; decide amend/suspend/EIS
- **Artifacts:** DRB, DVM, DRC (may be invalidated by output)

#### E-E2 - Emergency stop required
- **Trigger:** severe incident, unacceptable harm risk imminent
- **Effect:** SUSPEND
- **Transition:** PERMITTED | EXPIRING → SUSPENDED
- **Required actions:** activate EIS (B conditional, C mandatory); record activation; start recovery
- **Artifacts:** EIS activation record, DRB (B/C)

#### E-E3 - Reachability drill failed
- **Trigger:** escalation/EIS drill fails to meet requirements
- **Effect:** INVALIDATE (or SUSPEND if immediate stop required)
- **Required actions:** remediate reachability; re‑test; reissue DRC
- **Artifacts:** Evidence refs (test), procedures, DRC

#### E-E4 - Real activation occurred
- **Trigger:** EIS activated in real event
- **Effect:** SUSPEND (already implied), plus mandatory recovery
- **Required actions:** DRB review; tighten boundaries if needed; reissue DRC before re‑enable
- **Artifacts:** EIS, DRB, DRC, claim renewal

### F) Reference Evolution Events (GTAF Reference Changes)
#### E-F1 - Reference MINOR update adopted
- **Trigger:** scope adopts new GTAF minor reference version
- **Effect:** REVIEW_REQUIRED
- **Required actions:** confirm no semantic break; migrate optional fields if desired
- **Artifacts:** RCR, artifact revisions optional

#### E-F2 - Reference MAJOR update adopted
- **Trigger:** scope adopts new GTAF major reference version
- **Effect:** REVIEW_REQUIRED → often INVALIDATE until migrated (recommended)
- **Required actions:** migration plan; reissue DRC; reissue claim
- **Artifacts:** RCR, migrated artifacts, DRC(s), claim(s)

## Recommended event-to-blocker mapping (quick reference)
- E-C2 → EXPIRED_ARTIFACT:DRC
- E-C4 → EVIDENCE_EXPIRED
- E-D1/E-D2 → BOUNDARY_CHANGED_REQUIRES_REVALIDATION
- E-D5 → MANDATE_CHANGED_REQUIRES_REVALIDATION
- E-D7 → AMBIGUOUS_AUTHORIZATION / AMBIGUOUS_OUTCOME_OWNERSHIP
- E-E3 → REACHABILITY_NOT_VERIFIED

## Guardrails
- Don’t create “local event codes” without cataloging them (avoid fragmentation).
- Don’t treat drift signals as optional in Class C—bias to suspension.
- Don’t keep delegation running after INVALIDATE/SUSPEND triggers “because it’s inconvenient.”
