# Assessment-Models

**The independent ecosystem for OpenDEA-compatible maturity models, assessment models, assessment tools, and reusable assessment components.**

Assessment-Models governs, publishes, integrates and validates independently managed assessment assets. Each model lives in its own repository, with its own releases, issues, roadmap and contributors — integrated through versioned contracts, a central registry, and automated ecosystem CI.

## Relationship to OpenDEA

Assessment-Models **does not own the OpenDEA metamodel**. The canonical engineering authority is [`technehub-labs/dea-metamodel`](https://github.com/technehub-labs/dea-metamodel), which publishes the versioned contracts (assessment, maturity model, maturity scale, scoring, conformance, benchmark) that every asset in this organization declares conformance to.

```
technehub-labs/dea-metamodel          Assessment-Models
  Engineering Authority                 Ecosystem Authority
  publishes contracts          ─────►   registers & validates
                                        conformant assets
```

The dependency is **contractual, not structural**: models here consume a pinned, immutable contract release; the metamodel evolves independently.

## How to find models

The **[assessment-registry](https://github.com/Assessment-Models/assessment-registry)** is the integration spine. It answers: what exists, where it lives, which version is active, which contract it conforms to, which components it reuses, and how models relate to each other. Registry references are immutable (release / tag / commit SHA — never `main` or `latest`).

## Repository taxonomy

| Prefix | Contents | Examples |
|---|---|---|
| `maturity-model-*` | Independently versioned maturity models | `maturity-model-digital-transformation` |
| `assessment-model-*` | Independently versioned assessment models | — |
| `assessment-tool-*` | Assessment instruments and tooling | — |
| `maturity-components` | Reusable, versioned component packages (dimensions, criteria, level expectations, evidence requirements) | — |
| `assessment-registry` | Ecosystem integration spine (metadata + references only) | — |
| `assessment-ci` | Cross-repository validation and ecosystem integration logic | — |

## How models conform

Every asset declares a machine-readable **contract handshake** — the OpenDEA contract id + version it supports — validated by three CI levels:

1. **Local model CI** — syntax, schema validation, reference integrity, tests (in each model repo)
2. **Contract conformance CI** — validation against the declared dea-metamodel contract release
3. **Ecosystem CI** — cross-repository references, mappings, dependencies, compatibility (via assessment-registry + assessment-ci)

## How to contribute

See [CONTRIBUTING.md](../CONTRIBUTING.md) and [GOVERNANCE.md](../GOVERNANCE.md). Models are proposed via the registry; each accepted model gets its own repository and independent lifecycle. Component reuse is explicit (import / extend / override) and never imports scoring or scale semantics silently.

---

*Established under [CR-AM-11 — Federated Assessment Model Ecosystem](https://github.com/technehub-labs/dea-metamodel/blob/main/change-requests/CR-AM-11.md) (umbrella: CR-AM-01, OpenDEA Assessment Metamodel Evolution).*
