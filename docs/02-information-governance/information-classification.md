# Information Classification

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. Classification labels in this project apply to synthetic data only. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [data-ownership.md](data-ownership.md), [crown-jewels.md](crown-jewels.md)

## Purpose

Define how Lazarus Biotechnologies labels information so handling, storage, and sharing rules are consistent.

## Classification levels

| Level | Description | Examples | Default handling |
| --- | --- | --- | --- |
| Public | Intended for unrestricted release | Marketing site copy, published papers | No special controls |
| Internal | Business useful, not for public release | Org charts, non-sensitive runbooks, this repo's non-secret docs | Repo OK; no public posting of drafts marked otherwise |
| Confidential | Harmful if disclosed; limited audience | Contracts, unpublished research summaries, detection logic, architecture internals | Need-to-know; local-first; no secrets in git |
| Restricted | Highest sensitivity; statutory, safety, or existential IP risk | Patient/subject data, authentic credentials, unpublished crown-jewel IP, real HR PII | Not in git; encrypted local store or approved system only |

When unsure, classify one level higher and ask the data owner.

## Handling rules

- **Public:** May leave the organization.
- **Internal:** Default for project documentation in this repository.
- **Confidential:** Store in-repo only if stripped of secrets; screenshots must be redacted.
- **Restricted:** Never commit. Do not place in `screenshots/`, `portfolio/`, or chat logs.

See [ADR-001](../decisions/ADR-001-local-first.md) for where files live.

## Labeling

Documents should state classification near the top when they are Confidential or Restricted. Unlabeled files in `docs/` are treated as Internal.

## Mapping to crown jewels

Crown jewels are Confidential or Restricted by definition. The inventory is in [crown-jewels.md](crown-jewels.md).
