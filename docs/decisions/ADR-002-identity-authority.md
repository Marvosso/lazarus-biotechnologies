# ADR-002 — Identity Authority

**Status:** Accepted  
**Date:** 2026-09-21  
**Supersedes:** None

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All systems, identities, and access described in this decision are synthetic. No actual classified information, CUI, patient information, government data, or customer data is used.

## Context

Lazarus Biotechnologies needs business identities, technical identities,
lifecycle management, and future security simulation.

If Microsoft Entra ID (or another identity platform) is treated as the
sole source of truth, employment status, managers, and program
assignments become difficult to reconcile. If HR and IAM datasets are
kept completely independent, joiner/mover/leaver failures cannot be
detected as control failures.

The architecture must support realistic JML, access reviews, and later
stale-access scenarios without planting those failures in Day 0.

## Decision

Company-state / HR data is authoritative for employee identity.

Technical identity platforms consume that business state. They do not
become the source of truth for employment status or organizational
relationships.

Program assignments remain separate from organizational roles.
Department membership does not grant program access.

Fifty modeled employees does not require fifty live cloud accounts.
Modeled, active technical, privileged, and service identities remain
distinguishable.

## Alternatives Considered

### Identity platform as sole source of truth

Create and maintain people, departments, and access only in Entra.

Rejected because employment status, program assignments, and
reconciliation findings would have no independent business record.

### Completely independent HR and IAM datasets

Keep PostgreSQL and Entra as unrelated inventories.

Rejected because drift would be uninterpretable: it would not be clear
whether a mismatch is a data-quality issue or a security-control
failure.

### Company-state authoritative, IAM consuming

HR/company state defines who the person is. IAM provisions and
authenticates technical identities from that state. Program assignments
are a separate authorization source.

Selected.

## Rationale

This option enables realistic JML, reconciliation, access governance,
and security-failure scenarios. A terminated employee who remains
enabled in Entra is a finding, not a spreadsheet inconsistency.

It also explains why Lazarus uses more than manual Entra user creation.

## Security Implications

Synchronization and reconciliation become security-relevant.

Privileged identities stay separate from everyday accounts.

Day 0 remains least-privilege. Lifecycle failures are introduced later
by simulation, not by planting known-bad accounts at deployment.

Scenario ground truth must remain separate from analyst-facing evidence.

## Cost Implications

Modeled identities can exist without paid cloud seats. Live Entra
accounts are used only where they provide educational value, consistent
with ADR-001 and the $0 recurring-cost target / $10 soft ceiling.

## Consequences

Synchronization and reconciliation logic will eventually be necessary.

Identity telemetry must be correlatable with company-state employee
records.

Access reviews, mover removals, and leaver verification depend on this
split remaining intact.
