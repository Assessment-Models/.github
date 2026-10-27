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

### Legacy-naming exception (CR-AM-11 Phase 0 pre-federation repositories)

Repositories that predate the federation (est. CR-AM-11, 2026-08) and carry the `dea-` prefix are **recognized under their existing names**:

| Repository | Taxonomy class (recognized as) | Status |
|---|---|---|
| `dea-catalog-maturity-models` | Legacy catalog (no taxonomy equivalent) | Legacy — frozen, superseded by the v2 canonical maturity architecture (CR-AM-01 Release 1 D-1) |
| `dea-catalog-assessment-tools` | Assessment tools umbrella | Legacy — index demoted to registry view |
| `dea-assessment-modernization` | `assessment-model-<domain>` | Active — federated, registered, `v1.1.0-alpha` |
| `dea-assessment-technology` | `assessment-model-<domain>` | Active — federated, registered, `v1.1.0-alpha` |
| `dea-assessment-operations` | `assessment-model-<domain>` | Active — federated, registered, `v1.1.0-alpha` |
| `dea-assessment-services-delivery` | `assessment-model-<domain>` | Active — federated, registered, `v1.1.0-alpha` |

Rules for these repositories:

1. **No rename required.** Their registration records, release tags, pinned workflow references and registration-record references are all anchored to the current names; renaming would churn immutable references for no semantic gain (GitHub redirects preserve links but not tag-pinned workflow `uses` pins).
2. **New repositories MUST use the taxonomy naming** (`assessment-model-<domain>`, `maturity-model-<domain>`, `assessment-tool-<name>`); the exception is closed to new entrants.
3. **A migration (rename) may accompany a substantive migration** (e.g. a v1-alpha instrument porting to v2-canonical content) — at that point the taxonomy name is used for the new repository and the old one is registered with machine-readable supersession (CR-AR-05).
4. **Assets are identified by registration id, not repository name** — the registry is the identity spine; repository names are locations.

## Lifecycle conventions

Each model repository is independently versioned, released, tested, documented and governed. No model requires a shared repository release. Conformance is declared via the machine-readable contract handshake (CR-AM-11 §15) and validated by the three-level CI model (§14).

## Legacy repository classification (CR-AM-11 §26, Phase 0 initial table)

Classification states: **Legacy**, **Candidate for Migration**, **Reference**, **Deprecated**, **Superseded**. Classification is metadata only — no content moves until Phase 6, and then only per the IDENTIFY → CLASSIFY → EXTRACT → NORMALIZE → VALIDATE → REGISTER → RELEASE pipeline (§27).

| Repository | Classification | Rationale | Disposition |
|---|---|---|---|
| `dea-catalog-maturity-models` | **Legacy** | v1-alpha historical catalog; the v2 maturity scale is canonical in dea-metamodel (CR-AM-09). | **Decided — CR-AM-01 Release 1 D-1: frozen as legacy**, superseded by the v2 canonical maturity architecture; machine-readable supersession via CR-AR-05. Registered `status: legacy`. |
| `dea-catalog-assessment-tools` | **Legacy** | Catalog-of-tools shape superseded by the `assessment-tool-*` taxonomy; index demoted to a registry view with CI cross-checks. | Registered `status: legacy`; supersession declared via CR-AR-05. Shared schema/rubric remain consumable. |
| `dea-assessment-modernization` | **Active** (was Candidate for Migration) | Federated 2026-10-27: `model.yaml` handshake, Level 1/2 CI, registered, released `v1.1.0-alpha`. | Registered `status: active`; deliberately scores against the frozen v1-alpha scheme (D-1/D-3); per-domain v2 migration is incremental via new `maturity-model-*` repos. |
| `dea-assessment-technology` | **Active** (was Candidate for Migration) | Federated 2026-10-27 (same pattern). | Same as modernization. |
| `dea-assessment-operations` | **Active** (was Candidate for Migration) | Federated 2026-10-27 (same pattern). | Same as modernization. |
| `dea-assessment-services-delivery` | **Active** (was Candidate for Migration) | Federated 2026-10-27 (same pattern). | Same as modernization. |

Classification table refreshed 2026-10-27 after ecosystem integration (registry population, federation, Level 3 CI) and the CR-AM-01 Release 1 decision. The authoritative live classification is the registry's `status` field, cross-checked by ecosystem CI; this table is the documentation view.

No repository is destructively rewritten as a first step; the architecture supports coexistence (§26).

## Baseline CI policies

- Every model repository runs **Level 1 local CI** on every PR: syntax, schema validation, reference integrity, internal consistency, version consistency, examples, tests.
- **Level 2 contract conformance CI** validates the declared contract version against the pinned dea-metamodel release.
- **Level 3 ecosystem CI** (assessment-registry + assessment-ci) validates cross-repository references, mappings, dependencies, compatibility and duplicate identifiers.
- All three levels are demonstrated by the same first model (CR-AM-11 §31).
- Cross-repository fan-out requires the org-level dispatch credential (CR-AM-11 Phase 1 prerequisite); until it exists, fan-out workflows are `workflow_dispatch`-only.
