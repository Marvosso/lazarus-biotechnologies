# ADR-004 — Hyper-V Virtualization Platform

**Status:** Accepted  
**Date:** 2026-09-21  
**Supersedes:** None

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This decision applies to a simulated enterprise lab. No actual classified information, CUI, patient information, government data, or customer data is used.

## Context

Lazarus Biotechnologies requires a local virtualization platform capable
of supporting representative Windows and Linux systems, segmented
virtual networks, checkpoints, resource controls, and future automation.

The physical host runs Windows 11 Pro with hardware virtualization
enabled. A Microsoft hypervisor environment is already present and VBS
is active.

Host assessment identified memory as the primary physical constraint.

## Considered Options

### Microsoft Hyper-V

Advantages:

- Native Windows integration
- No additional recurring cost
- Strong PowerShell management
- Virtual-switch support
- Dynamic Memory
- Checkpoints
- Compatible with the existing Microsoft virtualization environment

### VMware Workstation

Advantages:

- Mature desktop virtualization
- Strong VM-management capabilities
- Flexible networking

Disadvantages for the current project:

- Requires an additional virtualization platform
- No identified V0.1 requirement that justifies introducing it

### VirtualBox

Advantages:

- Free
- Cross-platform
- Straightforward desktop virtualization

Disadvantages for the current project:

- Less attractive integration with the existing Windows virtualization
  environment
- Hyper-V provides stronger native PowerShell administration for the
  project's objectives

## Decision

Lazarus Biotechnologies V0.1 will use Microsoft Hyper-V as its primary
virtualization platform.

Hyper-V is selected because it is the best fit for this architecture on
this host, not because it is universally the best hypervisor.

## Rationale

Hyper-V satisfies the V0.1 technical requirements while integrating with
the existing Windows host and supporting future PowerShell automation.

Dynamic Memory is also valuable because host assessment identified RAM
as the project's primary physical constraint.

This also avoids installing VMware or VirtualBox when they do not solve
a V0.1 requirement better.

## Security Implications

Convenience networking (including Default Switch) must not define
Lazarus security zones. Cyber-range isolation remains an architecture
requirement. Checkpoints are not backups.

## Cost Implications

No additional recurring cost. Matches the $0 operating-cost target.

## Consequences

Infrastructure documentation and automation will initially target
Hyper-V.

A future architecture revision may select another virtualization
platform if Hyper-V creates a material technical limitation.

## VM Generation Standard

New Lazarus virtual machines will use Hyper-V Generation 2 by default.

Generation 1 will only be used where a documented compatibility
requirement exists.

## Memory Allocation Standard

Dynamic Memory may be used for compatible general-purpose virtual
machines to reduce host memory pressure.

Security platforms, databases, and other memory-sensitive workloads will
be evaluated individually rather than automatically configured with
Dynamic Memory.

Actual memory utilization will be measured after deployment.
