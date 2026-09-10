# Roadmap

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All people, programs, data, and incidents in this project are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

**Status:** Draft  
**Related:** [project-charter.md](project-charter.md), [scope-and-constraints.md](scope-and-constraints.md)

Work proceeds in layers: define the project, define the company, govern the information, then build architecture and supporting tooling.

## Phase 0 — Project definition

- [x] Repository layout
- [x] Project charter, scope, and roadmap
- [ ] Confirm owners and success criteria

## Phase 1 — Company baseline

- [x] Company profile
- [x] Organizational structure
- [x] Workforce roster (template)
- [ ] Fill roster and org chart with approved names/roles only

## Phase 2 — Information governance

- [x] Information classification
- [x] Data ownership
- [x] Crown jewels
- [ ] Map each crown jewel to an owner, system, and control set

## Phase 3 — Architecture and decisions

- [x] ADR-001: local-first
- [ ] Architecture overview in `docs/architecture/`
- [ ] Further ADRs as choices are made (identity, logging, backup, etc.)

## Phase 4 — Tooling and evidence

- [ ] Infrastructure definitions
- [ ] Simulator scenarios aligned to crown jewels
- [ ] Detection content
- [ ] Scripts for repeatable local workflows
- [ ] Screenshots and portfolio artifacts with secrets stripped

## Later / backlog

- Formal review cadence for docs
- Changelog discipline as documents stabilize
- Decision log beyond ADR-001

## Change policy

Update this file when a phase completes or when scope in [scope-and-constraints.md](scope-and-constraints.md) changes. Record notable releases in `/CHANGELOG.md`.
