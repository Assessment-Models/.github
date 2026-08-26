# Security Policy

## Reporting a vulnerability

Please report security issues privately to the organization maintainers via GitHub Security Advisories on the affected repository, or by contacting the technehub-labs OpenDEA maintainers. Do not open public issues for vulnerabilities.

## Scope

- Model and component content in this organization is data (YAML/JSON conforming to OpenDEA contracts); the primary integrity risks are malformed references, supply-chain drift in CI, and non-immutable external references.
- Registry references must be immutable (tag / SHA / digest). CI jobs must pin action versions by commit SHA.
- The org-level dispatch credential (CR-AM-11 Phase 1) is scoped to `repository_dispatch` only and stored as an organization secret; it is never printed in logs.

## Supported versions

Each model repository supports its latest minor release line. The registry records which version of each asset is active (CR-AM-11 §10–12).
