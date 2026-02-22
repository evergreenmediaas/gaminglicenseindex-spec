# GamingLicenseIndex (GLI) — Public Specification

GamingLicenseIndex (GLI) is a deterministic, read-only regulatory verification registry for the iGaming industry.

This repository contains the **public specification layer only**.

It documents the structural models and governance principles used by the GamingLicenseIndex system.  
It does not contain any ingestion pipelines, scraping logic, scoring mechanisms, ranking systems, internal APIs, or database architecture.

The purpose of this repository is institutional transparency and long-term auditability.


## Scope

This repository defines:

- JSON schemas for:
  - Regulator
  - Operator
  - License
- Status classification model:
  - VALID
  - EXPIRED
  - SUSPENDED
  - UNCLEAR
- Deterministic validation principles
- Negative signal handling policy
- Versioning model
- Example (non-production) dataset


## Design Philosophy

GamingLicenseIndex is built on the following principles:

- Deterministic data modeling  
- Explicit status states  
- Read-only registry behavior  
- No rankings or recommendations  
- Machine-readable structure  
- Transparent provenance  
- Explicit versioning and timestamps  

The system is intentionally conservative and designed to be citation-safe.


## Explicit Non-Scope

This repository does **not** include:

- Scrapers or crawlers  
- Parsing engines  
- Canonical mapping logic  
- Internal verification workflows  
- Affiliate logic  
- Commercial systems  
- Infrastructure implementation  

All implementation layers remain private.


## Governance

GamingLicenseIndex is operated exclusively by Evergreen Media AS.

Governance decisions prioritize:

- Accuracy over growth  
- Stability over expansion  
- Auditability over automation  


## Versioning

Specification changes follow semantic versioning.

Each release will document:

- Schema revisions  
- Status model updates  
- Methodology adjustments  
- Changelog entries  
