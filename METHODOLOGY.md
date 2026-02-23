# Methodology

GamingLicenseIndex operates on deterministic, manual verification principles.

This document defines the structural rules and validation logic used by the system.

---

## Core Principles

### 1. Deterministic Resolution

Same input → same output.

When an operator has multiple licenses, license selection follows a fixed priority:

```
1. Prefer license with status VERIFIED
2. Else first license with non-UNCLEAR status
3. Else first license by created_at (ascending)
```

This rule is **immutable** and **deterministic**.

### 2. Manual Verification Only

All license data is sourced from **publicly available regulator records**.

Verification is performed manually against official regulator registries.

**No automated scraping is specified** in this document.

### 3. Snapshot-Based, Not Real-Time

License data reflects the **most recent snapshot** from regulator sources.

The system does **not** provide real-time verification.

`last_verified` timestamps indicate when data was last confirmed against regulator records.

### 4. No Enrichment, No Inference

If data is not present in the official regulator record, it is **not included**.

**No fuzzy matching.**  
**No name aliasing.**  
**No cross-regulator inference.**

Only explicit, verifiable data is recorded.

### 5. Default to UNCLEAR

When verification fails or data is ambiguous, status defaults to `UNCLEAR`.

This is **not a judgment** — it reflects absence of verifiable data.

---

## Data Source Policy

### Primary Source

**Malta Gaming Authority (MGA)** public registry.

- Official URL: `https://authorisation.mga.org.mt/verification.aspx`
- Data is sourced from the publicly accessible verification portal

### Source Transparency

All license records include:

- `source_url` — direct link to regulator verification page
- `methodology_version` — specification version used for verification
- `last_verified` — ISO 8601 timestamp of last manual verification

### Source Validation

Source URLs must be:

- Publicly accessible (no authentication required)
- Official regulator domains only
- Stable and citation-safe

---

## Status Classification

See [STATUS_DEFINITIONS.md](STATUS_DEFINITIONS.md) for full taxonomy.

### Operator Status

```
REGISTERED — operator exists in regulator records
LISTED     — operator is actively listed in public registry
UNCLEAR    — operator verification inconclusive
```

### License Status

```
VERIFIED   — license confirmed active in regulator records
SUSPENDED  — license suspended by regulator
REMOVED    — license revoked or withdrawn
UNCLEAR    — license verification inconclusive
```

---

## License Selection Logic

When an operator has **multiple licenses**, the public API returns a **single license** using deterministic resolution.

### Resolution Rule

```typescript
function pickLicense(licenses) {
  // Step 1: Prefer VERIFIED
  const verified = licenses.find(l => l.status === "VERIFIED");
  if (verified) return verified;

  // Step 2: Else first non-UNCLEAR
  const nonUnclear = licenses.find(l => l.status !== "UNCLEAR");
  if (nonUnclear) return nonUnclear;

  // Step 3: Else first by created_at ASC
  const sorted = licenses.sort((a, b) => 
    new Date(a.created_at) - new Date(b.created_at)
  );
  return sorted[0];
}
```

### Multi-License Transparency

The **operator detail page** displays **all licenses** for full transparency.

The **verification API** returns **one license** using deterministic resolution.

These are **different surfaces** with different purposes.

---

## Negative Signal Handling

See [NEGATIVE_SIGNAL_POLICY.md](NEGATIVE_SIGNAL_POLICY.md).

When data conflicts or verification fails:

1. Default to `UNCLEAR`
2. Do not infer or assume
3. Document the uncertainty explicitly

---

## Methodology Version

Current methodology version: **v1.0**

All license records include a `methodology_version` field indicating which specification version was used for verification.

When methodology changes, the version increments according to [VERSIONING.md](VERSIONING.md).

---

## Non-Methodology

This specification does **not** define:

- Scraping implementation
- Parsing logic
- Data ingestion workflows
- Storage architecture
- API rate limiting
- Caching strategies
- Update frequency

These are implementation details and remain private.
