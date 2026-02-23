# Versioning Policy

GamingLicenseIndex follows **semantic versioning** for this specification.

## Version Format

```
MAJOR.MINOR.PATCH
```

### MAJOR

Breaking changes to schema structure or status definitions.

**Examples:**
- Removing required fields
- Changing field types
- Renaming status values
- Restructuring schema hierarchy

### MINOR

Backward-compatible additions or clarifications.

**Examples:**
- Adding optional fields
- Adding new status values (without removing existing)
- Adding enum options
- Clarifying methodology documentation

### PATCH

Non-functional changes with no schema impact.

**Examples:**
- Documentation corrections
- Example data updates
- README clarifications
- Typo fixes

---

## Current Version

**1.0.0** (February 2026)

Initial public specification release.

---

## Backwards Compatibility

### Schema Evolution

When schemas evolve:

1. **Required fields are never removed** in MINOR or PATCH versions
2. **Field types are never changed** in MINOR or PATCH versions
3. **New optional fields may be added** in MINOR versions
4. **Enum values may be added** (not removed) in MINOR versions

### Deprecation Policy

If a field must be deprecated:

1. **Deprecation notice** is added in MINOR version (field remains functional)
2. **Removal** occurs in next MAJOR version (minimum 6 months after deprecation)

---

## Methodology Versioning

The `methodology_version` field in license records follows this specification version.

**Current methodology version:** `v1.0`

When methodology changes:
- **Breaking methodology changes** → MAJOR version increment
- **Clarifications or minor adjustments** → MINOR version increment

---

## Status Definition Versioning

Status value definitions are **immutable** within a MAJOR version.

Adding new status values → MINOR version  
Changing status definitions → MAJOR version

---

## Changelog

All version changes are documented in [CHANGELOG.md](CHANGELOG.md).

Each entry must include:
- Version number
- Release date
- Change type (MAJOR / MINOR / PATCH)
- Detailed change description
- Migration guidance (if breaking)

---

## Version Guarantees

Within the same MAJOR version:

✅ **Guaranteed:**
- Existing field names remain unchanged
- Existing field types remain unchanged
- Required fields remain required
- Status value meanings remain stable

❌ **Not Guaranteed:**
- New optional fields may appear
- New status values may appear
- Documentation may be clarified or expanded

---

## Release Cadence

This specification has **no fixed release schedule**.

Versions are released only when:
- Schema adjustments are required
- Methodology changes are formalized
- Status definitions need clarification

The specification prioritizes **stability over frequent updates**.
