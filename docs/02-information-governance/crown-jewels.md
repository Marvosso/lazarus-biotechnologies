# Crown Jewels

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. Crown-jewel assets listed here are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [information-classification.md](information-classification.md), [data-ownership.md](data-ownership.md)

## Purpose

Name the assets whose loss, theft, or integrity failure would cause severe harm to Lazarus Biotechnologies. Architecture, simulator scenarios, and detections should prioritize these first.

## Inventory

| ID | Asset | Why it is a crown jewel | Owner | Classification | System / location | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| CJ-001 | Unpublished research IP | Competitive and scientific core | R&D | Restricted | TBD | Protocols, sequences, results not yet public |
| CJ-002 | Quality / regulatory record set | Product credibility and legal standing | Quality / Regulatory | Confidential / Restricted | TBD | Integrity matters as much as secrecy |
| CJ-003 | Identity and privileged access | Keys to every other jewel | IT / Security (custodian) | Restricted | TBD | Credentials never in git |
| CJ-004 | Workforce records | Legal duty; high human harm | HR | Restricted | `data/hr/` (placeholders only) | Real PII out of repo |
| CJ-005 | Backup and recovery capability | Ransomware and integrity attacks | IT / Security | Confidential | TBD | Availability of CJ-001–CJ-004 |
| CJ-006 | Detection content and logging | Early warning and evidence | Security lead | Confidential | `detections/` | Protect from tampering and leak of defensive logic |

Add or split rows as architecture is defined. Do not list live hostnames, account names, or secret material here.

## Use in this project

- **Architecture:** Controls are designed around this list, not around tools.
- **Simulator:** Scenarios should state which crown jewel is at risk.
- **Detections:** High-severity detections map to CJ-003, CJ-005, and CJ-006 at minimum.
- **Portfolio / screenshots:** Show the model and redacted evidence, never the Restricted payload.

## Review

Revisit this inventory when the org chart changes, when a new system of record appears, or after a tabletop that finds an undocumented jewel.
