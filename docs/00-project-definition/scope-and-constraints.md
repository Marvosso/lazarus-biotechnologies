# Scope and Constraints

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All people, programs, data, and incidents in this project are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [project-charter.md](project-charter.md), [roadmap.md](roadmap.md)

## In scope

- Company definition: profile, organizational structure, workforce roster
- Information governance: classification, data ownership, crown jewels
- Architecture notes and architecture decision records (ADRs)
- Local working data under `data/` (HR and governance)
- Infrastructure definitions, simulator work, detections, scripts, screenshots, and portfolio artifacts that support this project

## Out of scope

- Production clinical, manufacturing, or patient-care systems
- Live customer, patient, or employee personal data in this repository
- Cloud-first SaaS as the system of record for sensitive project material (see [ADR-001](../decisions/ADR-001-local-first.md))
- Legal advice, regulatory filings, or certified audit opinions
- Work that requires writing exploits, malware, or attack procedures

## Constraints

| Constraint | Implication |
| --- | --- |
| Local-first | Authoritative files live in this repo and on the local workstation unless an ADR says otherwise |
| No secrets in git | Credentials, keys, and real PII stay out of version control |
| Documentation before tooling | Charter, company, and governance docs precede simulator and detection work |
| Least invention | Treat unspecified company facts as TBD rather than assuming production systems exist |
| Evidence hygiene | Screenshots and portfolio material must not contain live secrets or real personal data |

## Assumptions

- Lazarus Biotechnologies is the reference organization for this repository.
- Documents in `docs/` are the canonical narrative; `data/` holds structured working copies.
- Architecture and detections will be designed against the crown jewels and classification scheme, not the other way around.

## Open questions

- [ ] Who is the named project owner and information owner?
- [ ] Which environments (if any) will exist beyond local files?
- [ ] What legal/regulatory baseline applies (HIPAA, GDPR, GxP, other)?
