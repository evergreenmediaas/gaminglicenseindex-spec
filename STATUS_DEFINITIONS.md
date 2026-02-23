# Status Definitions

GamingLicenseIndex uses explicit, deterministic status taxonomies for operators and licenses.

---

## Operator Status

### `REGISTERED`

Operator exists in regulator records but may not be actively listed.

**Criteria:**
- Operator appears in official regulator database
- Legal entity is registered with regulator
- May or may not have active licenses

### `LISTED`

Operator is actively listed in public regulator registry.

**Criteria:**
- Operator has publicly accessible registry entry
- Operator is explicitly listed as active in regulator records

### `UNCLEAR`

Operator verification is inconclusive.

**Criteria:**
- Operator name is ambiguous or cannot be matched
- Regulator records are inconsistent or incomplete
- Verification failed for technical or access reasons

**Important:** `UNCLEAR` is **not a judgment** about legitimacy.  
It reflects absence of verifiable data only.

---

## License Status

### `VERIFIED`

License is confirmed active in regulator records.

**Criteria:**
- License appears in official regulator verification portal
- License has active/valid status in regulator records
- Source URL is publicly accessible and citation-safe
- Verification timestamp is recent

**Does NOT imply:**
- Legal compliance
- Operational status
- Service quality
- Regulatory approval of operator activities

### `SUSPENDED`

License is suspended by regulator.

**Criteria:**
- Regulator explicitly marks license as suspended
- License is not revoked, but temporarily inactive
- Suspension is documented in official regulator records

### `REMOVED`

License is revoked, withdrawn, or no longer valid.

**Criteria:**
- License has been formally revoked by regulator
- License has been voluntarily surrendered
- License has expired and not been renewed
- License no longer appears in active regulator records

### `UNCLEAR`

License verification is inconclusive.

**Criteria:**
- License data is ambiguous or incomplete
- Regulator records conflict with other sources
- Source URL is inaccessible or unreliable
- Verification failed for technical or access reasons

**Important:** `UNCLEAR` is **not a negative signal**.  
It reflects uncertainty in verification only.

---

## Status Transitions

### Operator Status Transitions

```
UNCLEAR → REGISTERED  (verification succeeded)
UNCLEAR → LISTED      (active listing confirmed)
REGISTERED → LISTED   (public listing confirmed)
LISTED → UNCLEAR      (verification failed)
```

### License Status Transitions

```
UNCLEAR → VERIFIED    (verification succeeded)
VERIFIED → SUSPENDED  (regulator suspended license)
VERIFIED → REMOVED    (license revoked/withdrawn)
SUSPENDED → VERIFIED  (suspension lifted)
SUSPENDED → REMOVED   (suspension became permanent)
REMOVED → VERIFIED    (license reinstated, rare)
* → UNCLEAR           (verification failed)
```

---

## Status Immutability

Within a specification MAJOR version, status **values** are immutable.

**Status meanings do not change.**

New status values may be **added** in MINOR versions.

Existing status values are **never renamed or redefined** within a MAJOR version.

---

## Status vs. Compliance

### What Status IS

- Factual observation of regulator record state
- Snapshot-based verification result
- Deterministic classification

### What Status IS NOT

- Legal compliance judgment
- Operational status indicator
- Recommendation or endorsement
- Real-time regulatory status

---

## Default Status

When verification fails or data is missing:

**Default: `UNCLEAR`**

This is a **conservative default** that avoids false positives.

---

## Status Source

All status values are derived from:

1. **Official regulator records** (primary source)
2. **Manual verification** (no automated inference)
3. **Publicly accessible data** (no privileged access)

Status is **never inferred** from:
- Third-party databases
- Operator websites
- Commercial data providers
- Affiliate networks
