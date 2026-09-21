# ADR-003 — Architecture Baseline v0.1

**Status:** Accepted  
**Date:** 2026-09-21  
**Supersedes:** None

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This decision applies to a simulated enterprise. No actual classified information, CUI, patient information, government data, or customer data is used.

## Context

Lazarus Biotechnologies has completed initial enterprise architecture
design covering business requirements, logical systems, networking,
identity, data flows, security controls, and observability.

Implementation requires a stable reference architecture while still
allowing changes when real technical constraints are discovered.

## Decision

Architecture v0.1 is approved as the initial implementation baseline.

Material deviations discovered during implementation will be documented
rather than silently rewriting the original design.

## Alternatives Considered

### Keep architecture informal and update files in place

Rejected because design history, constraints, and lessons would be lost.

### Freeze architecture as unchangeable

Rejected because host capacity and implementation testing will almost
certainly require revision.

### Versioned baseline with ADRs for material change

Selected.

## Rationale

Maintaining architecture versions preserves:

- Design history
- Engineering reasoning
- Lessons learned
- Implementation constraints
- Portfolio evidence

## Security Implications

Security-control status remains Planned unless implementation and
verification have occurred. Preferred tools listed in the baseline are
not treated as deployed.

## Cost Implications

The $0 recurring-cost target and $10 soft ceiling remain in force.
Host assessment may force a smaller concurrent footprint rather than
paid cloud compute.

## Consequences

Architecture v0.1 may require revision after host assessment or
implementation testing.

Future architecture versions must identify what changed and why.
