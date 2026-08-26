# Governance — Assessment-Models Organization

Established by [CR-AM-11 — Federated Assessment Model Ecosystem](https://github.com/technehub-labs/dea-metamodel/blob/main/change-requests/CR-AM-11.md). Umbrella: CR-AM-01 (OpenDEA Assessment Metamodel Evolution).

## Architectural principle

**Centralize contracts, governance and integration; decentralize model ownership, lifecycle and evolution.**

| Decentralized (per model repo) | Centralized (org level) |
|---|---|
| Model content, scales, scoring logic | Model registration, conformance contracts |
| Releases, issues, roadmaps, contributors | Compatibility rules, reference resolution |
| | Cross-model validation, integration testing, ecosystem governance |

## Authority boundary

- **technehub-labs/dea-metamodel** is the canonical engineering authority for the OpenDEA metamodel, assessment/maturity semantics, schemas, conformance contracts, canonical vocabularies and validation specifications.
- **Assessment-Models** is the ecosystem authority for independently managed, OpenDEA-compatible assessment assets. It consumes versioned contracts; it does not redefine the metamodel.
- Cross-organization dependencies are **contractual** (pinned, immutable contract releases), never repository-structural. Git submodules are prohibited as an integration mechanism (CR-AM-11 §23).

## Repository taxonomy (CR-AM-11 §8)

| Repository class | Naming | Lifecycle |
|---|---|---|
| Organization defaults | `.github` (this repo) | Org-governed |
| Integration spine | `assessment-registry` | Org-governed |
| Ecosystem CI | `assessment-ci` | Org-governed |
| Reusable components | `maturity-components` | Independently versioned |
| Maturity models | `maturity-model-<domain>` | Independent: own releases, issues, roadmap |
| Assessment models | `assessment-model-<domain>` | Independent |
| Assessment tools | `assessment-tool-<name>` | Independent |

## Naming conventions

- Lowercase, hyphenated repository names; `<domain>` is a short singular domain slug (e.g. `digital-transformation`, `autonomous-operations`, `agentic-enterprise`).
- Every model repository carries a root `model.yaml` manifest declaring: identity, version, contract dependency, components, dependencies, compatibility (CR-AM-11 §22).
- Versions are SemVer; releases are git tags `vX.Y.Z`. Registry references must be immutable (tag / commit SHA / content digest — never `main`, `master`, `latest`; CR-AM-11 §12).

## Lifecycle conventions

Each model repository is independently versioned, released, tested, documented and governed. No model requires a shared repository release. Conformance is declared via the machine-readable contract handshake (CR-AM-11 §15) and validated by the three-level CI model (§14).

## Legacy repository classification (CR-AM-11 §26, Phase 0 initial table)

Classification states: **Legacy**, **Candidate for Migration**, **Reference**, **Deprecated**, **Superseded**. Classification is metadata only — no content moves until Phase 6, and then only per the IDENTIFY → CLASSIFY → EXTRACT → NORMALIZE → VALIDATE → REGISTER → RELEASE pipeline (§27).

| Repository | Classification | Rationale | Disposition |
|---|---|---|---|
| `dea-catalog-maturity-models` | **Legacy** | v1-alpha historical catalog; the v2 maturity scale is canonical in dea-metamodel (CR-AM-09). Historical models preserved. | Selected models migrated individually in Phase 6. Open `docs/maturity-scoring-v2-proposal` PR closed as superseded by the canonical CR-AM-09 scale contract. |
| `dea-catalog-assessment-tools` | **Legacy** | Catalog-of-tools shape superseded by the `assessment-tool-*` taxonomy. | Content migration candidate, Phase 6. |
| `dea-assessment-modernization` | **Candidate for Migration** | Domain assessment content, dormant since 2026-07-22. | Migrate to `assessment-model-*` / `maturity-model-*` in Phase 6. |
| `dea-assessment-technology` | **Candidate for Migration** | Domain assessment content, dormant since 2026-07-22. | Migrate in Phase 6. |
| `dea-assessment-operations` | **Candidate for Migration** | Domain assessment content, dormant since 2026-07-22. | Migrate in Phase 6. |
| `dea-assessment-services-delivery` | **Candidate for Migration** | Domain assessment content, dormant since 2026-07-22. | Migrate in Phase 6. |

No repository is destructively rewritten as a first step; the architecture supports coexistence (§26).

## Baseline CI policies

- Every model repository runs **Level 1 local CI** on every PR: syntax, schema validation, reference integrity, internal consistency, version consistency, examples, tests.
- **Level 2 contract conformance CI** validates the declared contract version against the pinned dea-metamodel release.
- **Level 3 ecosystem CI** (assessment-registry + assessment-ci) validates cross-repository references, mappings, dependencies, compatibility and duplicate identifiers.
- All three levels are demonstrated by the same first model (CR-AM-11 §31).
- Cross-repository fan-out requires the org-level dispatch credential (CR-AM-11 Phase 1 prerequisite); until it exists, fan-out workflows are `workflow_dispatch`-only.
