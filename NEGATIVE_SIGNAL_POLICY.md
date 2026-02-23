# Negative Signal Policy

GamingLicenseIndex follows a **conservative uncertainty handling model**.

When data conflicts or verification fails, the system defaults to explicit uncertainty rather than making assumptions.

---

## Core Principle

**Default to `UNCLEAR` when uncertain.**

This policy prioritizes **accuracy over coverage** and **caution over inference**.

---

## What Triggers UNCLEAR

### License Status → UNCLEAR

When any of the following occur:

1. **Source URL is inaccessible**
   - Regulator verification portal is down
   - Source page returns 404 or authentication error
   - URL structure has changed

2. **Data conflicts exist**
   - Multiple regulator records show different status
   - License ID appears in multiple contradictory contexts
   - Operator name does not match license holder exactly

3. **Verification fails technically**
   - Manual verification process encounters errors
   - Regulator portal is temporarily unavailable
   - Data extraction cannot be completed reliably

4. **License data is ambiguous**
   - License ID format is unclear or non-standard
   - Jurisdiction field is missing or inconsistent
   - Multiple operators claim the same license

5. **No verifiable data exists**
   - License does not appear in regulator records
   - Operator is not found in regulator database
   - Brand cannot be mapped to legal operator entity

### Operator Status → UNCLEAR

When any of the following occur:

1. **Operator name is ambiguous**
   - Multiple entities with similar names exist
   - Legal name does not match regulator records exactly
   - Operator uses multiple legal entities

2. **Regulator records are incomplete**
   - Operator appears in partial records only
   - Registration data is missing key fields
   - Operator status field is empty or unrecognized

3. **Verification cannot be completed**
   - Regulator database is inaccessible
   - Manual verification process fails
   - Source data is corrupted or unreadable

---

## What DOES NOT Trigger UNCLEAR

The following do **not** automatically result in `UNCLEAR`:

- Operator has multiple licenses (uses deterministic resolution)
- License has old `last_verified` timestamp (status remains stable until re-verified)
- Source URL is slow to load (as long as data is retrievable)
- Regulator website design changes (as long as data is still accessible)

---

## UNCLEAR vs. REMOVED

**Important distinction:**

- **UNCLEAR** = verification inconclusive, uncertainty exists
- **REMOVED** = license explicitly revoked/withdrawn by regulator

If a regulator **explicitly states** a license is revoked → `REMOVED`  
If a license simply **does not appear** in records → `UNCLEAR`

**Never infer `REMOVED` from absence alone.**

---

## Conflicting Data Handling

### Scenario 1: Multiple Regulators

If an operator is licensed by multiple regulators:

- Each license is recorded separately
- No cross-regulator inference is performed
- Verification queries specify regulator context

### Scenario 2: Contradictory Status

If regulator records show conflicting status for the same license:

- Status is set to `UNCLEAR`
- Source URL points to the most authoritative record
- Conflict is documented in verification notes (internal)

### Scenario 3: Name Mismatch

If operator name in regulator records does not match queried brand:

- Status is set to `UNCLEAR` (no fuzzy matching)
- Brand-to-operator mapping must be explicit
- Canonical names are never inferred

---

## Re-Verification Policy

When a license is marked `UNCLEAR`:

1. Manual re-verification is attempted
2. If re-verification succeeds → status updated to appropriate value
3. If re-verification fails again → remains `UNCLEAR`
4. `last_verified` timestamp is updated regardless

**No automatic retry logic is specified.**

---

## Transparency Requirement

When `UNCLEAR` status is returned via API:

- `source_url` may be `null` (if source is unavailable)
- `methodology_version` is always present
- `last_verified` reflects last verification attempt

The API **does not explain why** verification was unclear (this is internal).

---

## False Positive Prevention

The system prioritizes **avoiding false VERIFIED classifications**.

**Better to return `UNCLEAR` than incorrectly mark a license as `VERIFIED`.**

This conservative approach protects citation integrity.

---

## User Communication

When displaying `UNCLEAR` status:

**Recommended messaging:**

> "License verification inconclusive. Users must verify directly with the regulator."

**NOT recommended:**

> "This operator is unlicensed."  
> "License status unknown — proceed with caution."

`UNCLEAR` is **not a warning** — it is a factual statement about verification limits.

---

## Non-Policy

This policy does **not** define:

- How long to wait before retrying verification
- How many verification attempts to perform
- Which regulator sources take precedence
- How to handle regulator outages

These are operational decisions and remain internal.
