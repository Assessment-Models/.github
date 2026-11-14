# Enterprise & Organization Assessment Models

**The independent ecosystem for maturity models, assessment models, assessment tools, and reusable assessment components.**  
Use these assets on their own or in tandem with OpenDEA to drive enterprise maturity and targeted capability improvement.

Assessment-Models governs, publishes, integrates, and validates independently managed assessment assets. Each model lives in its own repository—with its own releases, issues, roadmap, and contributors—integrated through versioned contracts, a central registry, automated ecosystem CI, and a shared repository standard.

**Status:** Early ecosystem • 19 public repositories • MIT licensed • OpenDEA-compatible

## Who this is for

Enterprise architects, capability leads, transformation owners, and builders of assessment tooling who need versioned, machine-readable maturity and assessment assets.

## What’s in the ecosystem right now

### Maturity models (`maturity-model-*`)
- [maturity-model-digital-transformation](https://github.com/Assessment-Models/maturity-model-digital-transformation) — Composite Digital Transformation maturity model (first-model candidate demonstrating all three CI levels)
- [maturity-model-digital-transformation-operationalized](https://github.com/Assessment-Models/maturity-model-digital-transformation-operationalized) — Operationalized Digital Transformation model
- [maturity-model-modernization](https://github.com/Assessment-Models/maturity-model-modernization) — Architecture Modernization
- [maturity-model-technology](https://github.com/Assessment-Models/maturity-model-technology) — Technology
- [maturity-model-operations](https://github.com/Assessment-Models/maturity-model-operations) — Operations
- [maturity-model-services-delivery](https://github.com/Assessment-Models/maturity-model-services-delivery) — Services Delivery
- [maturity-model-autonomous-operations](https://github.com/Assessment-Models/maturity-model-autonomous-operations) — Autonomous Operations

### Standards & scaffolding
- [maturity-model-standard](https://github.com/Assessment-Models/maturity-model-standard) — Normative repository standard, schemas, reusable conformance workflow, and portfolio conformance registry
- [maturity-model-template](https://github.com/Assessment-Models/maturity-model-template) — GitHub template for new `maturity-model-*` repositories

### Integration & validation
- [assessment-registry](https://github.com/Assessment-Models/assessment-registry) — Ecosystem integration spine (what exists, where it lives, which version is active, which contract it conforms to, which components it reuses)
- [assessment-ci](https://github.com/Assessment-Models/assessment-ci) — Cross-repository validation and ecosystem integration logic
- [maturity-components](https://github.com/Assessment-Models/maturity-components) — Reusable maturity component packages

### Catalogs & assessment tools
- [dea-catalog-maturity-models](https://github.com/Assessment-Models/dea-catalog-maturity-models) — Enterprise Architecture maturity models catalog
- [dea-catalog-assessment-tools](https://github.com/Assessment-Models/dea-catalog-assessment-tools) — Architecture assessment tools catalog
- Domain assessment tools: [dea-assessment-modernization](https://github.com/Assessment-Models/dea-assessment-modernization), [dea-assessment-technology](https://github.com/Assessment-Models/dea-assessment-technology), [dea-assessment-operations](https://github.com/Assessment-Models/dea-assessment-operations), [dea-assessment-services-delivery](https://github.com/Assessment-Models/dea-assessment-services-delivery)

## Domains currently covered

Digital Transformation (composite + operationalized) · Architecture Modernization · Technology · Operations · Services Delivery · Autonomous Operations · plus supporting catalogs, components, and infrastructure.

## Quick start

1. **Discover assets** — Start with the [assessment-registry](https://github.com/Assessment-Models/assessment-registry). Registry references are immutable (release / tag / commit SHA — never `main` or `latest`).
2. **Understand the standard** — Read [maturity-model-standard](https://github.com/Assessment-Models/maturity-model-standard).
3. **Create a new model** — Use [maturity-model-template](https://github.com/Assessment-Models/maturity-model-template) and declare conformance via a root `standard.yaml`.
4. **Contribute** — See [CONTRIBUTING.md](../CONTRIBUTING.md) and [GOVERNANCE.md](../GOVERNANCE.md). Propose models via the registry.

## Relationship to OpenDEA

Assessment-Models **does not own the OpenDEA metamodel**. The canonical engineering authority is [`technehub-labs/dea-metamodel`](https://github.com/technehub-labs/dea-metamodel), which publishes the versioned contracts (assessment, maturity model, maturity scale, scoring, conformance, benchmark) that every asset in this organization declares conformance to.

```
technehub-labs/dea-metamodel          Assessment-Models
  Engineering Authority                 Ecosystem Authority
  publishes contracts          ─────►   registers & validates
                                        conformant assets
```

The dependency is **contractual, not structural**: models here consume a pinned, immutable contract release; the metamodel evolves independently.

## Repository taxonomy

| Prefix / Repo | Contents | Current examples |
|---|---|---|
| `maturity-model-*` | Independently versioned maturity models | digital-transformation, modernization, operations, technology, services-delivery, autonomous-operations, digital-transformation-operationalized |
| `assessment-model-*` | Independently versioned assessment models | (none yet) |
| `assessment-tool-*` | Assessment instruments and tooling | (none yet — see `dea-assessment-*` catalogs) |
| `maturity-components` | Reusable, versioned component packages (dimensions, criteria, level expectations, evidence requirements) | [maturity-components](https://github.com/Assessment-Models/maturity-components) |
| `assessment-registry` | Ecosystem integration spine (metadata + references only) | [assessment-registry](https://github.com/Assessment-Models/assessment-registry) |
| `assessment-ci` | Cross-repository validation and ecosystem integration logic | [assessment-ci](https://github.com/Assessment-Models/assessment-ci) |
| `maturity-model-standard` | Normative repository standard, schemas, reusable conformance workflow, portfolio conformance registry | [maturity-model-standard](https://github.com/Assessment-Models/maturity-model-standard) |
| `maturity-model-template` | GitHub template repository implementing the repository standard | [maturity-model-template](https://github.com/Assessment-Models/maturity-model-template) |

## How models conform

Every asset declares a machine-readable **contract handshake** — the OpenDEA contract id + version it supports — validated by three CI levels:

1. **Local model CI** — syntax, schema validation, reference integrity, tests (in each model repo)
2. **Contract conformance CI** — validation against the declared dea-metamodel contract release
3. **Ecosystem CI** — cross-repository references, mappings, dependencies, compatibility (via assessment-registry + assessment-ci)

Every maturity-model repository additionally declares adoption of the **[AM-MODEL-REPOSITORY-STANDARD](https://github.com/Assessment-Models/maturity-model-standard)** in a root `standard.yaml` (repository type, standard version, conformance level: registered → structural → full), validated by a reusable conformance workflow that also enforces version coherence across `standard.yaml`, `model.yaml`, `VERSION`, and the README. New maturity-model repositories are created from [`maturity-model-template`](https://github.com/Assessment-Models/maturity-model-template).

## How to contribute

See [CONTRIBUTING.md](../CONTRIBUTING.md) and [GOVERNANCE.md](../GOVERNANCE.md). Models are proposed via the registry; each accepted model gets its own repository and independent lifecycle. Component reuse is explicit (import / extend / override) and never imports scoring or scale semantics silently.

---

*Established under [CR-AM-11 — Federated Assessment Model Ecosystem](https://github.com/technehub-labs/dea-metamodel/blob/main/change-requests/CR-AM-11.md) (umbrella: CR-AM-01, OpenDEA Assessment Metamodel Evolution). Extended by [CR-AM-ORG-RES-000 — Organization-Wide Maturity Model Repository Standardization, Architecture and Global Conformance](https://github.com/Assessment-Models/maturity-model-standard/blob/main/change-requests/CR-AM-ORG-RES-000.md).*
