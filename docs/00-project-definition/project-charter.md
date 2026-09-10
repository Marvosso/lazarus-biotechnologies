# Project Charter

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used.

**Project:** Lazarus Biotechnologies documentation and control environment  
**Status:** Draft  
**Owner:** TBD

## Purpose

Establish a single, local-first source of truth for how Lazarus Biotechnologies is defined, governed, and operated. This repository holds company context, information-governance rules, architecture decisions, and supporting artifacts used to design, simulate, and evidence controls.

## Problem

Without a shared charter, company facts, data ownership, and technical decisions live in scattered notes. That makes it hard to:

- Agree on scope and constraints
- Classify and protect sensitive information
- Trace architecture choices back to business need
- Produce consistent evidence for portfolio, audit, or tabletop work

## Objectives

1. Document the company, organization, and workforce baseline.
2. Define information classification, ownership, and crown-jewel assets.
3. Record architecture and operating decisions as ADRs.
4. Keep sensitive work local by default (see [ADR-001](../decisions/ADR-001-local-first.md)).
5. Provide a durable home for simulator, detection, infrastructure, and portfolio artifacts.

## In scope

See [scope-and-constraints.md](scope-and-constraints.md).

## Out of scope

See [scope-and-constraints.md](scope-and-constraints.md).

## Success criteria

- Folder layout and core definition documents exist and are current.
- Classification, ownership, and crown-jewel lists are explicit enough to drive control design.
- Major technical choices are captured as ADRs rather than tribal knowledge.
- A reader new to the repo can start in this folder and understand what the project is and is not.

## Stakeholders

| Role | Responsibility |
| --- | --- |
| Project owner | Charter, scope, roadmap, and final decisions |
| Information owner | Classification, ownership, and crown jewels |
| Technical owner | Architecture, infrastructure, simulator, detections |
| Reviewers | Challenge assumptions; confirm documents are usable |

## Timeline

See [roadmap.md](roadmap.md).

## Related documents

- [Scope and constraints](scope-and-constraints.md)
- [Roadmap](roadmap.md)
- [Company profile](../01-company/company-profile.md)
- [ADR-001 Local-first](../decisions/ADR-001-local-first.md)
