# ADR-005 — Virtual Firewall and Router

**Status:** Accepted  
**Date:** 2026-09-21  
**Supersedes:** None

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This decision applies to a simulated enterprise lab. No actual classified information, CUI, patient information, government data, or customer data is used.

## Context

The Lazarus network architecture requires controlled communication
between security zones.

Hyper-V private switches provide Layer 2 isolation but do not provide
routing, firewall enforcement, or Internet connectivity.

The three initial zones (`LBT-USER`, `LBT-SERVER`, `LBT-SECURITY`) are
deployed and verified. Without a router they cannot reach each other or
the Internet.

## Considered Options

### Windows host routing and NAT

Would make the physical laptop the implicit enterprise router and attach
host authority to every zone.

### Linux-based router/firewall

Viable, but would require assembling routing, NAT, and logging from
scratch rather than using a dedicated firewall platform.

### pfSense

Capable firewall/router. Not selected for V0.1; OPNsense provides
equivalent capability with a fit we prefer for this lab.

### OPNsense

Dedicated virtual firewall/router with stateful policy, NAT, routing,
and logging.

Selected.

## Decision

Lazarus V0.1 will use a dedicated OPNsense virtual machine as the
enterprise router and firewall.

The VM name will be `LBT-FW-01`.

This ADR does not authorize downloading an ISO or creating the VM.
Acquisition and deployment are a later implementation step.

## Architecture

The firewall will connect to the Hyper-V Default Switch for upstream
connectivity.

Lazarus security zones will connect to dedicated private Hyper-V
switches.

Enterprise workloads must not use the Hyper-V Default Switch as a
shortcut around the Lazarus firewall.

```
Internet
   │
Windows Host
   │
Hyper-V Default Switch   = WAN / upstream
   │
   │ WAN
   ▼
LBT-FW-01
   │
   ├── LBT-USER       10.10.10.1
   ├── LBT-SERVER     10.10.20.1
   └── LBT-SECURITY   10.10.40.1
```

MGMT, RANGE, and DMZ remain undeployed until required. RANGE will be a
separate controlled boundary.

## Rationale

A dedicated firewall provides:

- Explicit trust boundaries
- Stateful firewall policy
- Network segmentation
- Routing
- NAT
- Security logging
- Future network-security exercises
- Stronger portfolio evidence

The approach also prevents the physical Windows host from serving as the
implicit enterprise router.

## Resource Constraint

LBT-FW-01 must remain lightweight because host memory is the primary
physical constraint.

Initial target:

- Generation 2
- 2 vCPU
- Approximately 2 GB RAM
- Approximately 20 GB dynamically expanding storage

Actual utilization will be measured after deployment.

## Security Implications

Initial policy will be restrictive. USER must not reach SECURITY or
MANAGEMENT by default. USER to SERVER will be specific services only
(for example HTTPS, not PostgreSQL). Rules are not implemented in this
ADR.

Firewall logs should eventually feed observability.

## Cost Implications

OPNsense is free. Recurring cost remains $0. RAM budget comes from the
8–10 GB Lazarus envelope (HOST-001).

## Consequences

Infrastructure deployment must verify installer source and integrity
before creating `LBT-FW-01`.

Default Switch remains WAN-only for the firewall, not a general Lazarus
LAN.
