# Comparison Lens

This section is meant to be fast to read and precise. It avoids “framework bingo” and highlights the structural delta GTAF introduces.

### ISO/IEC 42001 (AI Management System)
- **Optimizes for:** a management‑system layer: policies, objectives, roles, continual improvement for responsible AI.
- **Assumes:** governance intent can be translated into operational controls and sustained via management processes.
- **Leaves implicit:** a formal “permission‑to‑delegate” gate with boundary/authority/ownership semantics.
- **How GTAF closes the gap:** GTAF turns “govern AI” into artifact closure + DRC binary gating: SB/DR/RB are prerequisites; DRC becomes the deterministic readiness verdict within scope/version/window.
- **Integration handshake:** use ISO 42001 as governance umbrella; GTAF provides delegation semantics beneath it (especially for agentic/autonomous operations).

### NIST AI RMF 1.0
- **Optimizes for:** risk‑management vocabulary and structure (GOVERN/MAP/MEASURE/MANAGE).
- **Assumes:** organizations tailor the framework; actions are guidance, not a checklist.
- **Leaves implicit:** deterministic authorization/ownership boundaries at delegation time; a formal “this delegation is permitted” artifact.
- **How GTAF closes the gap:** GTAF introduces per‑context delegation closure (DC tuple) and a derived DRC gate; AI RMF stays “risk reasoning,” GTAF becomes “delegation permission semantics.”
- **Integration handshake:** map AI RMF GOVERN outcomes to GTAF artifact requirements (SB/DR/RB/DRC) and lifecycle controls (DRB/EIS/DVM).

### EU AI Act (Post-Market Monitoring, High-Risk)
- **Optimizes for:** regulatory lifecycle obligations including post‑market monitoring and documentation.
- **Assumes:** providers can implement monitoring and corrective/preventive actions with adequate documentation.
- **Leaves implicit:** normalized internal structure for who may delegate what and who owns outcomes in autonomous contexts.
- **How GTAF closes the gap:** GTAF provides an internal control plane: DRB (review regime), EIS (intervention authority), DVM (early warning), tied to SB/DR/RB/DRC.
- **Integration handshake:** use GTAF artifacts as part of the internal governance evidence map supporting monitoring/response obligations.

### ISO/IEC 27001 (ISMS)
- **Optimizes for:** security management via ISMS requirements and auditability.
- **Assumes:** risks are managed via controls and continual improvement; scope is explicitly defined.
- **Leaves implicit:** decision authority and delegation semantics as first‑class objects.
- **How GTAF closes the gap:** GTAF adds a governance‑architecture layer: SB (liability/authority boundaries), DR (delegable decision spaces), RB (outcome ownership), DRC (readiness gate).
- **Integration handshake:** keep ISO 27001 for security controls; use GTAF to make decision authority/ownership explicit within the ISMS scope boundaries.

### Zero Trust Architecture (NIST SP 800-207 / 800-207A)
- **Optimizes for:** continuous verification, reducing implicit trust and static perimeter thinking.
- **Assumes:** resources, identities, and policies can be modeled and enforced continuously.
- **Leaves implicit:** who legitimately defines decision spaces and delegation authority; ZTA answers access, not delegation permission.
- **How GTAF closes the gap:** GTAF is “zero trust for authority”: it verifies decision authority, ownership, and intervention reachability, not just identity‑to‑resource access.
- **Integration handshake:** ZTA enforces access policies; GTAF ensures the authority to define/enact those policies is legitimate and bounded.

### AWS Well-Architected Framework
- **Optimizes for:** architectural quality and tradeoffs (pillars) and review discipline.
- **Assumes:** architectures can be evaluated using best‑practice questions and iterated.
- **Leaves implicit:** decision authority binding and delegation semantics when AI/automation makes changes fast.
- **How GTAF closes the gap:** GTAF makes who may decide a first‑class, versioned object (DR + RB) tied to a boundary (SB) with a gate (DRC).
- **Integration handshake:** use Well‑Architected for workload review; use GTAF to anchor who can approve/automate each tradeoff and under what intervention model.

### RAPID (Bain) and similar decision-rights frameworks
- **Optimizes for:** clarity of decision roles to reduce organizational friction.
- **Assumes:** clear role assignment improves decision effectiveness and accountability.
- **Leaves implicit:** technical boundaries, delegation levels, kill‑switch reachability, evidence‑based readiness.
- **How GTAF closes the gap:** GTAF binds decision rights to technical/system boundaries and turns readiness into a binary gate (DRC).
- **Integration handshake:** RAPID can be used inside DR authoring to clarify contributors; GTAF ensures the DR is delegable, bounded, and owned.

### Open Policy Agent (OPA) / Policy-as-Code engines
- **Optimizes for:** consistent enforcement of authorization policies via declarative evaluation.
- **Assumes:** policies exist, are expressible, and enforcement points consult a policy engine.
- **Leaves implicit:** who is authorized to define policy, how policy relates to liability boundaries, who owns outcomes, and whether delegation is permitted at all.
- **How GTAF closes the gap:** GTAF sits above OPA: it defines authority/ownership and valid delegation contexts in which a policy engine may operate.
- **Integration handshake:** OPA can enforce constraints derived from DR/SB (optional). GTAF remains tool‑agnostic; the key is that “policy exists” becomes “policy is legitimate and bounded.”
