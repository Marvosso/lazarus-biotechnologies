# ADR-001: Local-first

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All systems, data, and decisions in this project are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Accepted  
**Date:** 2026-09-10  
**Deciders:** Project owner (TBD)

## Context

Lazarus Biotechnologies documentation includes company structure, information governance, and later simulator, detection, and portfolio material. Some of that material will be Confidential. Restricted data (real PII, credentials, unpublished IP payloads) must not become someone else's system of record by default.

A cloud-first approach (wiki, SaaS GRC, shared drives as primary) would split truth across vendors, increase accidental exposure, and make it harder to keep Restricted data out of the workstream.

## Decision

This project is **local-first**.

1. The git repository on the local workstation is the system of record for Internal documentation and for Confidential material that has been stripped of secrets.
2. Restricted data does not go in git, screenshots, or portfolio exports.
3. Cloud services are optional conveniences (remote backup of the repo, collaboration), not the place where crown jewels are born or stored.
4. New tools (simulator, detections, infrastructure) default to local execution and local files unless a later ADR supersedes this one.

## Consequences

### Positive

- One tree to read: `docs/`, `data/`, `infrastructure/`, `simulator/`, `detections/`
- Easier classification enforcement: if it is in git, it must be fit for git
- Architecture and evidence stay portable for portfolio work
- Fewer implicit vendors in the trust boundary

### Negative

- Collaboration requires git discipline rather than a live shared doc
- Backup and device protection become the operator's problem
- Real Restricted datasets need a separate, non-repo store if they are ever used

## Follow-ups

- Document backup/restore of the local repo in `docs/architecture/` when that folder is filled in
- Add ADRs if a specific cloud or lab environment is later required
- Keep [information-classification.md](../02-information-governance/information-classification.md) aligned with this decision
