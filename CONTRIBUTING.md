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
