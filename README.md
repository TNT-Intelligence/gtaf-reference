# GTAF Reference
Official reference publication of the Governance & Trust Architecture Framework (GTAF).

GTAF is a **normative, artifact‑centric framework** for delegation in complex technical systems. It defines the minimum structural prerequisites that must be true before delegation is permitted.

## Status
This repository is the **normative reference**. Current reference version: **v0.1.1**.  
If you need to make or interpret conformity claims, always bind them to **(Scope, Reference Version, Validity Window)**.

## Public Availability
- The public repository `gtaf-reference` is publicly readable as a standalone reference.
- The MkDocs site is publicly reachable (e.g., `gtaf.tnt-intelligence.com`) and reflects the current working state of the reference.

## Scope
This repository contains:
- the authoritative definitions of GTAF artifacts
- the core rules/invariants and lifecycle semantics
- risk classes and minimum requirements
- non-normative application examples and illustrative guidance

## Non‑Goals
GTAF is **not**:
- an implementation guide
- a tooling platform
- a certification scheme

## How To Read
Suggested order:
1. Core Model (`docs/01-core-model/overview.md`)
2. Artifacts (`docs/02-artifacts/`)
3. Rules & Invariants (`docs/03-rules/`)
4. Lifecycle (`docs/04-lifecycle/`)
5. Risk & Criticality (`docs/05-risk-and-criticality/`)
6. Terminology (`docs/10-terminology/glossary.md`)

## Quick Start (Docker)
Build and start the docs server:
```sh
docker compose up -d --build
```

Open:
```text
http://localhost:8000
```

Stop:
```sh
docker compose down
```

## Optional: Run Locally (No Docker)
Prereqs:
- Python 3.12+
- MkDocs + MkDocs Material
- pymdown-extensions (required by `mkdocs.yml`)

```sh
pip install mkdocs mkdocs-material pymdown-extensions watchdog
mkdocs serve --dev-addr=0.0.0.0:8000
```

## Editing
All content lives under `docs/`. With Docker Compose running, edits to `.md` files
are live‑reloaded automatically.

## Docker Image (Release)
A GitHub Actions workflow builds and publishes a Docker image on each published release:
- Image: `ghcr.io/tnt-intelligence/gtaf-reference`
- Tags: the release tag

## Repository Structure
- `docs/`: GTAF reference content (MkDocs source)
- `mkdocs.yml`: navigation and site config
- `Dockerfile`, `docker-compose.yml`: dev environment for docs

## Governance & Change Control
Reference evolution is controlled and versioned. See:
- `docs/11-versions/versioning-and-change-control.md`
- `docs/00-meta/governance-of-the-reference.md`

## Releases & Citation
- Tagged releases follow `vMAJOR.MINOR.PATCH` (e.g., `v0.1.0`).
- Each tagged release is archived by Zenodo and assigned:
  - a version DOI
  - a concept DOI
  - Citation instructions describe the DOI-based citation scheme applied to released versions. See `docs/00-meta/citation-and-versioning.md`.

## License
See `LICENSE`.
