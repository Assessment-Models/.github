# Change Requests — Assessment-Models Organisation (`.github`)

This index tracks organisation-level Change Requests (CRs) of the **ORG-RES** (Organisation Resolution) series. The `.github` repository is the normative home of organisation-level governance (CR-AM-ORG-RES-001 §15); organisation CRs of this series land here.

| CR | Title | Status | Canonical location |
|----|-------|--------|--------------------|
| CR-AM-ORG-RES-000 | Organization-Wide Maturity Model Repository Standardization, Architecture and Global Conformance | Accepted (organization resolution) | [`maturity-model-standard/change-requests/CR-AM-ORG-RES-000.md`](https://github.com/Assessment-Models/maturity-model-standard/blob/main/change-requests/CR-AM-ORG-RES-000.md) |
| [CR-AM-ORG-RES-001](CR-AM-ORG-RES-001.md) | Assessment-Models Organisation Charter, Authority and Decision Rights | **Proposed** | this repository — [`change-requests/CR-AM-ORG-RES-001.md`](CR-AM-ORG-RES-001.md) |

---

## Convention notes

- **Series naming**: `CR-AM-ORG-RES-NN.md`. The ORG-RES series is distinct from the upstream `technehub-labs/dea-metamodel` `CR-AM-NN` sequence (the `CR-AM-12` slot there is occupied by an unrelated change; see CR-AM-ORG-RES-000 §0 and CR-AM-ORG-RES-001 §0).
- **Status values**: `Proposed` → `Accepted` → `Implemented` → `Superseded`.
- **Land-as-authored**: the file in `change-requests/` is the authoritative decision record, byte-identical to the originating attachment. Supplementary rationale is linked, not duplicated.
- **Cross-repository entries**: CRs whose canonical home is another repository (e.g. CR-AM-ORG-RES-000 in `maturity-model-standard`) are listed here with a link to the source of truth rather than copied, to avoid divergence.

## How to add a CR

1. Author the CR doc following the ORG-RES structure (header attribute table, numbered sections, decision/approval record).
2. Land it in `change-requests/CR-AM-ORG-RES-NN.md` — for organisation-level governance, this repository is the normative location (CR-AM-ORG-RES-001 §15).
3. Add a row to the table above.
4. Open a PR.
