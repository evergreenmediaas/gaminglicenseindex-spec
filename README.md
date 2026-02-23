# GamingLicenseIndex (GLI) — Public Specification

GamingLicenseIndex (GLI) is a deterministic, read-only regulatory verification registry for the iGaming industry.

This repository contains the **public specification layer only**.

It documents the structural models and governance principles used by the GamingLicenseIndex system.  
It does **not** contain any ingestion pipelines, scraping logic, scoring mechanisms, ranking systems, internal APIs, or database architecture.

The purpose of this repository is institutional transparency and long-term auditability.

---

## Repository Structure

```
gaminglicenseindex-spec/
├── README.md                      (this file)
├── LICENSE                        (MIT License)
├── VERSIONING.md                  (semantic versioning policy)
├── METHODOLOGY.md                 (deterministic validation principles)
├── STATUS_DEFINITIONS.md          (license and operator status taxonomy)
├── NEGATIVE_SIGNAL_POLICY.md      (uncertainty handling)
├── schemas/
│   ├── operator.schema.json       (operator data model)
│   ├── regulator.schema.json      (regulator data model)
│   └── license.schema.json        (license data model)
├── examples/
│   ├── operator.example.json      (dummy operator data)
│   ├── regulator.example.json     (dummy regulator data)
│   └── license.example.json       (dummy license data)
└── CHANGELOG.md                   (specification version history)
```

---

## Scope

This repository defines:

* JSON schemas for:
  * Regulator
  * Operator
  * License
* Status classification model:
  * `VERIFIED`
  * `SUSPENDED`
  * `REMOVED`
  * `UNCLEAR`
* Deterministic validation principles
* Negative signal handling policy
* Versioning model
* Example (non-production) dataset

---

## Design Philosophy

GamingLicenseIndex is built on the following principles:

* **Deterministic data modeling** — same input always produces same output
* **Explicit status states** — no ambiguous or inferred statuses
* **Read-only registry behavior** — verification only, no licensing authority
* **No rankings or recommendations** — factual data projection only
* **Machine-readable structure** — JSON schemas with strict typing
* **Transparent provenance** — source URLs and methodology versions
* **Explicit versioning and timestamps** — all data snapshot-based

The system is intentionally conservative and designed to be citation-safe.

---

## Explicit Non-Scope

This repository does **not** include:

* Scrapers or crawlers
* Parsing engines
* Canonical mapping logic
* Internal verification workflows
* Affiliate logic
* Commercial systems
* Infrastructure implementation
* Database schemas or migrations
* API implementation details
* Scoring or ranking algorithms

All implementation layers remain private.

---

## Usage

This specification is intended for:

* Institutional transparency
* Third-party data model alignment
* Academic citation
* Regulatory audit trails
* Long-term documentation

It is **not** intended as:

* An open-source implementation
* A distributable codebase
* A reusable scraping framework

---

## Governance

GamingLicenseIndex is operated exclusively by **Evergreen Media AS**.

**Organization number:** 996 768 139  
**D-U-N-S® number:** 671343097  
**Registered in:** Norway  
**Contact:** post@evergreenmedia.no

Governance decisions prioritize:

* Accuracy over growth
* Stability over expansion
* Auditability over automation

---

## Versioning

Specification changes follow semantic versioning (MAJOR.MINOR.PATCH).

See [VERSIONING.md](VERSIONING.md) for details.

---

## License

This specification is released under the MIT License.

See [LICENSE](LICENSE) for details.

---

## Contributing

This is a **read-only specification repository**.

We do not accept pull requests, feature requests, or external contributions.

For questions or clarifications, contact: post@evergreenmedia.no
