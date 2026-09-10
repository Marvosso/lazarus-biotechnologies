# Data Ownership

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All data domains and ownership assignments in this project are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [information-classification.md](information-classification.md), [crown-jewels.md](crown-jewels.md), [organizational-structure.md](../01-company/organizational-structure.md)

## Purpose

Separate **who is accountable for the data** from **who operates the systems that hold it**.

## Roles

| Role | Meaning |
| --- | --- |
| Data owner | Accountable for classification, access policy, retention, and “who may use this” |
| Data custodian | Operates storage, backup, identity, logging, and technical controls |
| Data user | Accesses data to do a job; no ownership by access alone |

IT is usually custodian, not owner, of research, HR, and finance records.

## Ownership map

| Data domain | Owner function | Typical custodian | Default classification | Working location |
| --- | --- | --- | --- | --- |
| Research IP and protocols | R&D | IT | Confidential / Restricted | TBD; not in public docs |
| Quality and regulatory records | Quality / Regulatory | IT | Confidential | TBD |
| Workforce / HR | Human Resources | IT | Confidential / Restricted | `data/hr/` (no real PII) |
| Governance policies and inventories | Legal / Compliance (or project owner) | IT | Internal / Confidential | `data/governance/`, `docs/02-information-governance/` |
| Financial records | Finance | IT | Confidential | TBD |
| Logs, configs, detections | Security lead (custodian); owners remain with source domain | IT / Security | Internal / Confidential | `detections/`, `infrastructure/` |
| Identity and credentials | Data owner of the system of record | IT / Security | Restricted | Never in git |

Named people are filled in [workforce-roster.md](../01-company/workforce-roster.md).

## Rules

1. Every crown jewel has one owner function.
2. Custodians may refuse unsafe storage; they may not reclassify unilaterally.
3. Simulator and detection work must respect this map: compromise of a system is not transfer of ownership.

## Open questions

- [ ] Named owner for each row above
- [ ] Retention periods per domain
