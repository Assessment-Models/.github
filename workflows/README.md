# Baseline CI policy

The three-level CI model (CR-AM-11 §14):

1. **Level 1 — Local model CI** (in each model repo): syntax, schema validation, reference integrity, internal consistency, version consistency, documentation, examples, tests.
2. **Level 2 — Contract conformance CI**: each model declares a specific supported OpenDEA contract version (the contract handshake, §15); CI resolves the pinned dea-metamodel release and validates conformance.
3. **Level 3 — Ecosystem CI** (assessment-registry + assessment-ci): registry integrity, reference resolution, contract/version compatibility, component dependencies, cross-model mappings, scale interoperability, benchmark compatibility, duplicate identifiers (§13.1).

Reusable workflow implementations land with `assessment-ci` in **CR-AM-11 Phase 1**. Until the org-level dispatch credential exists, cross-repo fan-out workflows are `workflow_dispatch`-only (Phase 1 prerequisite — GITHUB_TOKEN cannot `repository_dispatch` across repositories).

Organization-level workflow templates will be added to this directory as the phases land.
