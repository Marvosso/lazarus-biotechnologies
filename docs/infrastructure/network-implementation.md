# Lazarus Lab Network Implementation

**Document ID:** LBT-INF-NET-001  
**Status:** Initial Layer-2 zones deployed; routing/firewall not implemented  
**Version:** 0.1  
**Phase:** 2 — Core Infrastructure  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This document describes simulated lab networking. No actual classified information, CUI, patient information, government data, or customer data is used.

Related: [network-architecture.md](../architecture/network-architecture.md),
[ADR-004](../decisions/ADR-004-hyper-v-platform.md),
[virtualization-standard.md](virtualization-standard.md).

## Purpose

This document records implementation of the Lazarus Biotechnologies
virtual network architecture on Microsoft Hyper-V.

The approved architecture defines six logical security zones.

Initial infrastructure deployment activates only the zones required by
current workloads.

A virtual switch is Layer 2 connectivity. It is not a firewall. Routing
and filtering will be enforced later by a dedicated virtual
router/firewall, not by creating empty switches for unused zones.

## Network Plan

| Zone | Hyper-V Switch | Subnet | Deployment |
| --- | --- | --- | --- |
| User | LBT-USER | 10.10.10.0/24 | Initial |
| Server | LBT-SERVER | 10.10.20.0/24 | Initial |
| Management | LBT-MGMT | 10.10.30.0/24 | Deferred |
| Security | LBT-SECURITY | 10.10.40.0/24 | Initial |
| Cyber Range | LBT-RANGE | 10.10.50.0/24 | Deferred |
| DMZ | LBT-DMZ | 10.10.60.0/24 | Deferred |

## Switch Naming

| Switch | Intended attachment |
| --- | --- |
| LBT-USER | LBT-WIN-01 |
| LBT-SERVER | LBT-INFRA-01 |
| LBT-SECURITY | LBT-SIEM-01 |
| LBT-MGMT | Deferred |
| LBT-RANGE | Deferred |
| LBT-DMZ | Deferred |

## Switch Type

Lazarus security zones use **Private** Hyper-V switches.

Private: VMs can communicate with each other on that switch. The Windows
host does not receive a virtual adapter on that network.

Internal would attach the physical host to every enterprise subnet and
blur lab-owner authority with simulated enterprise architecture.

The Hyper-V Default Switch remains unchanged and is not part of the
Lazarus enterprise topology.

## Addressing

Hyper-V switches do not create IP subnets. Addresses are assigned to
interfaces later.

Reserved gateways (not implemented yet):

| Zone | Gateway |
| --- | --- |
| USER | 10.10.10.1 |
| SERVER | 10.10.20.1 |
| MANAGEMENT | 10.10.30.1 |
| SECURITY | 10.10.40.1 |
| RANGE | 10.10.50.1 |
| DMZ | 10.10.60.1 |

IP convention remains:

| Range | Purpose |
| --- | --- |
| .1 | Gateway |
| .2–.9 | Network infrastructure |
| .10–.49 | Servers / infrastructure |
| .50–.99 | Expansion |
| .100–.199 | Clients / dynamic |
| .200–.239 | Testing |
| .240–.254 | Reserved |

DHCP is not deployed. Initial systems will use static addresses.

No routing, NAT, or firewall policy is implemented in this step.

A dedicated virtual firewall/router (candidates: OPNsense, pfSense,
Linux router/firewall) is preferred over host Windows routing. Selection
and install are deferred until Layer-2 networks exist.

## Implementation Record

### Initial State

Hyper-V contained only the Microsoft-managed Default Switch.

No Lazarus virtual networks existed.

### Changes Performed

Created three private Hyper-V switches (Administrator PowerShell,
2026-09-21):

- LBT-USER
- LBT-SERVER
- LBT-SECURITY

`Get-VM` remained empty. No virtual machines were created.

### Deferred Networks

The following architecture zones remain undeployed until required:

- LBT-MGMT
- LBT-RANGE
- LBT-DMZ

Cyber Range stays off until there is a workload that needs it. RANGE →
ENTERPRISE will be deny-by-default when it is implemented.

### Addressing

No IP addresses, gateways, DHCP services, routing, NAT, or firewall
policies have yet been implemented.

### Existing Hyper-V Networking

The Hyper-V Default Switch remains unchanged and is not part of the
Lazarus enterprise topology.

### Verification

`Get-VMSwitch | Sort-Object Name`:

| Name | SwitchType |
| --- | --- |
| Default Switch | Internal |
| LBT-SECURITY | Private |
| LBT-SERVER | Private |
| LBT-USER | Private |

`Get-NetAdapter` where Name like `*LBT*`: no adapters.

Private switches did not attach the physical host to USER, SERVER, or
SECURITY. That is the intended boundary.

Structured inventory: [network-inventory.csv](../../data/governance/network-inventory.csv).
