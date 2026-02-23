# Changelog

All notable changes to the GamingLicenseIndex specification will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-02-18

### Added

**Initial public specification release.**

- JSON schemas for:
  - `regulator.schema.json` (v1.0)
  - `operator.schema.json` (v1.0)
  - `license.schema.json` (v1.0)
- Status definitions:
  - Operator status: `REGISTERED`, `LISTED`, `UNCLEAR`
  - License status: `VERIFIED`, `SUSPENDED`, `REMOVED`, `UNCLEAR`
- Methodology documentation (v1.0)
  - Deterministic license resolution logic
  - Manual verification principles
  - Snapshot-based verification model
- Negative signal policy
  - UNCLEAR default when uncertain
  - Conservative uncertainty handling
- Versioning policy (semantic versioning)
- Example dataset (dummy/sanitized data)
- MIT License

### Governance

- Repository operated by Evergreen Media AS
- Read-only specification (no external contributions)
- Institutional transparency focus

---

## Future Versions

Future changes will be documented here with:

- **[MAJOR.MINOR.PATCH]** version number
- **Release date** (YYYY-MM-DD)
- **Added / Changed / Deprecated / Removed / Fixed** sections
- **Migration guidance** (for breaking changes)

---

## Versioning Rules

See [VERSIONING.md](VERSIONING.md) for full policy.

**MAJOR** = Breaking changes (schema structure, status definitions)  
**MINOR** = Backward-compatible additions (new fields, new status values)  
**PATCH** = Documentation fixes (no schema impact)
