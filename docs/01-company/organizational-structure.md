# Organizational Structure

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, and business activity in this project are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [company-profile.md](company-profile.md), [workforce-roster.md](workforce-roster.md)

## Purpose

Show how Lazarus Biotechnologies is organized so ownership of people, process, and data is unambiguous.

## Leadership

```
Chief Executive Officer
├── Research & Development
├── Quality / Regulatory
├── Information Technology (incl. security)
├── Human Resources
├── Finance
└── Legal / Compliance
```

Names and reporting lines are recorded in [workforce-roster.md](workforce-roster.md). Do not put real personal data in this file.

## Function responsibilities

| Function | Primary responsibility | Typical data it owns |
| --- | --- | --- |
| Executive | Strategy, risk appetite, final accountability | Board and strategy material |
| R&D | Science, pipeline, lab operations | Research IP, protocols, results |
| Quality / Regulatory | GxP, submissions, controlled documents | Quality records, regulatory files |
| IT / Security | Systems, identity, monitoring, backups | Logs, configs, credentials (custodian) |
| Human Resources | Workforce lifecycle | HR records (see `data/hr/`) |
| Finance | Accounts, contracts, spend | Financial records |
| Legal / Compliance | Contracts, privacy, investigations | Legal holds, policies |

Data-owner vs custodian rules are in [data-ownership.md](../02-information-governance/data-ownership.md).

## Information-governance alignment

- Each function has a named owner in the roster.
- Crown-jewel assets map to a function, not to a tool.
- Changes to this chart require a matching roster update.

## Open questions

- [ ] Confirm whether Clinical, Manufacturing, and Commercial exist as separate functions
- [ ] Confirm security reports to IT, CEO, or a dedicated CISO line
