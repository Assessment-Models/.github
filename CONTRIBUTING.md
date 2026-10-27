# Contributing to Assessment-Models

Thank you for your interest in the OpenDEA-compatible assessment ecosystem.

## Ground rules

1. **The metamodel is upstream.** Concepts, schemas, contracts and canonical vocabularies are owned by [`technehub-labs/dea-metamodel`](https://github.com/technehub-labs/dea-metamodel). Proposals that change the metamodel belong there as change requests — not in model repositories.
2. **Models declare conformance.** Every model repository carries a root `model.yaml` manifest with a machine-readable contract handshake (contract id + version). PRs that break the declared contract do not merge.
3. **References are immutable.** Cite releases, tags, commit SHAs or content digests — never `main` or `latest`.
4. **Reuse is explicit.** Components are referenced with a declared kind (`import` / `extend` / `override`). Reuse never silently imports scoring or scale semantics (CR-AM-11 §19–20).
5. **No git submodules** for ecosystem integration (CR-AM-11 §23). Integration is registry references + versioned releases + CI.

## Proposing a new model

1. Open an issue in [`assessment-registry`](https://github.com/Assessment-Models/assessment-registry) describing purpose, scope, intended contract version, and any component reuse.
2. On acceptance, a `maturity-model-<domain>` / `assessment-model-<domain>` / `assessment-tool-<name>` repository is created with the standard structure (CR-AM-11 §22).
3. Register the model's first release in the registry; Level 2 and Level 3 CI wire up from there.

## Repository conventions

Naming, taxonomy, lifecycle and the legacy classification table live in [GOVERNANCE.md](GOVERNANCE.md).

## The canonical contributor path (P4-3)

This is the end-to-end path every asset follows, demonstrated live by the
ecosystem's first wave (the four domain instruments, federated 2026-10-27).
All three CI levels are green on every merged asset today.

### 1. Propose (registry issue)

Open an issue in [`assessment-registry`](https://github.com/Assessment-Models/assessment-registry):
purpose, scope, intended contract version, and any component reuse. For a
new asset *class* or schema capability, land a CR first (see
[`change-requests/`](https://github.com/Assessment-Models/assessment-registry/tree/main/change-requests) — e.g. CR-AR-05 for machine-readable supersession).

### 2. Author the model repository (standard structure, CR-AM-11 §22)

```
<repo>/
├── model.yaml          ← the contract handshake (identity, version, contract, dependencies)
├── VERSION             ← SemVer, kept equal to model.yaml + instrument versions
├── <content>/          ← the model itself (instrument.yaml, scale, evaluation, …)
├── scripts/            ← Level 1 validation (structure + schema + consistency)
└── .github/workflows/
    ├── <local-ci>.yml          ← Level 1
    └── contract-conformance.yml ← Level 2 (reusable workflow, pinned)
```

The `model.yaml` handshake shape (see
[`maturity-model-digital-transformation`](https://github.com/Assessment-Models/maturity-model-digital-transformation/blob/main/model.yaml)
or any `dea-assessment-*` repo):

```yaml
id: <canonical-id>
type: maturity-model | assessment-model | assessment-tool
name: <human name>
version: X.Y.Z
conformance:
  contract:
    id: opendea-assessment-metamodel   # or a specific family id
  source:
    organization: technehub-labs
    repository: dea-metamodel
  version: "1.0"                       # exact / 1.x / ^1.0 / prefix — resolved by CI
dependencies:                          # other registered asset ids — immutable refs
  - id: <registered-asset-id>
    reference: vX.Y.Z
```

### 3. Release and register

1. Tag the release (`vX.Y.Z`) — tags are the preferred registry reference
   (commit SHAs work before the first tag).
2. Add the registration record: one YAML per asset under
   `registry/<type-dir>/<id>.yaml` — metadata + immutable reference only,
   never model content. `asset_class`, `status` (`active` once federated),
   and `superseded_by` if superseding another asset (CR-AR-05).
3. Registry CI validates: schema, immutable refs, unique ids, resolvable
   dependencies, type↔class coherence, supersession coherence.

### 4. The three CI levels (what runs, where)

| Level | Where | What it proves | Current green example |
|---|---|---|---|
| **1 — Local model CI** | the model repo, every PR | structure, schema, reference integrity, version consistency | `dea-assessment-*` `validate` job |
| **2 — Contract conformance** | the model repo, reusable workflow from `assessment-ci` | the handshake resolves against the published contract suite at the pinned metamodel release | `contract-conformance` job |
| **3 — Ecosystem CI** | `assessment-ci`, every PR | registry↔manifest coherence (id/type/version/contract at the pinned release), dependency resolution, immutable refs, catalog-view drift | `validate-ecosystem` + `catalog-view-check` jobs |

Level 2 wiring (copy into `.github/workflows/contract-conformance.yml`):

```yaml
jobs:
  contract-conformance:
    uses: Assessment-Models/assessment-ci/.github/workflows/contract-conformance.yml@main
    with:
      dea-metamodel-ref: <40-char SHA or vX.Y.Z — never main/latest>
      manifest-path: model.yaml
```

### 5. Verify and discover

- Resolve any asset: `assessment-registry/scripts/resolve.py <asset-id>`
  (prints source, version, pinned reference, contract, and supersession chain).
- Ecosystem health: `assessment-ci/scripts/validate_ecosystem.py --registry <registry-checkout>`.
- Legacy catalog consumers: the tools-umbrella index is a **generated view**
  (`assessment-ci/scripts/generate_catalog_view.py`); never hand-edit its
  domains — change the registry records and regenerate.

### Worked example (the four domain instruments)

1. Registered as `candidate-for-migration` at commit-SHA refs (registry PRs).
2. Federated: `model.yaml` handshakes + Level 1 scripts + Level 2 reusable
   workflows landed per repo (one PR each).
3. Tagged `v1.1.0-alpha`; registry records re-pointed at the tags.
4. Status flipped to `active` after the CR-AM-01 Release 1 decision (D-3).
5. Level 3 manifest-coherence checks activated automatically — the
   instruments' manifests are now verified against their registry records
   on every `assessment-ci` PR.

### What not to do

- **Don't rename pre-federation repositories** — see the legacy-naming
  exception in [GOVERNANCE.md](GOVERNANCE.md); identity is the registration
  id, not the repository name.
- **Don't hand-edit generated views** (the tools-umbrella index domains).
- **Don't pin mutable refs** (`main`/`latest`) anywhere — registry records,
  component references, workflow pins.
- **Don't register model content** in the registry — metadata and immutable
  references only (CR-AM-11 §11).
