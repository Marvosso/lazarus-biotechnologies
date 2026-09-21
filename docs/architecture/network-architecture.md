# Lazarus Biotechnologies Network Architecture

**Document ID:** LBT-ARCH-NET-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer.

## Purpose

This document defines the logical network architecture, addressing
standards, security zones, trust boundaries, and connectivity principles
for the Lazarus Biotechnologies virtual enterprise.

The network is designed to provide enterprise security concepts while
operating primarily on a single physical lab host.

The environment will not use a flat `192.168.1.0/24` lab. Logical
security zones exist so segmentation and trust boundaries remain part of
the architecture.

Physical VLANs, managed switches, and dedicated firewall appliances are
not required for v0.1. Hypervisor virtual networks can represent these
zones.

The v0.1 diagram is in
[diagrams/network-architecture-v0.1.md](diagrams/network-architecture-v0.1.md).

## Address Space

Lazarus laboratory networks use private RFC1918 address space.

Primary lab allocation:

`10.10.0.0/16`

Individual security zones use `/24` networks.

| Zone | Network | Purpose |
| --- | --- | --- |
| User | 10.10.10.0/24 | Representative employee endpoints |
| Server | 10.10.20.0/24 | Business applications and infrastructure |
| Management | 10.10.30.0/24 | Administrative and management functions |
| Security | 10.10.40.0/24 | Security monitoring and assessment |
| Cyber Range | 10.10.50.0/24 | Controlled security testing |
| DMZ / Future | 10.10.60.0/24 | Future externally accessible services |

Additional networks may be allocated from `10.10.0.0/16` as the
architecture evolves.

The `/24` size is for readability, not because 254 hosts are required:

| Third octet | Meaning |
| --- | --- |
| 10 | Users |
| 20 | Servers |
| 30 | Management |
| 40 | Security |
| 50 | Range |
| 60 | DMZ |

`10.10.40.12` should be recognizable as security infrastructure.

## Host Naming Convention

Lazarus systems use:

`LBT-[FUNCTION]-[NUMBER]`

Examples:

- LBT-WIN-01
- LBT-LNX-01
- LBT-APP-01
- LBT-DB-01
- LBT-ADMIN-01
- LBT-SIEM-01
- LBT-VULN-01
- LBT-RANGE-01

Names represent system function rather than a specific employee because
representative systems may serve multiple modeled users over time.

## IP Convention

Ranges inside each `/24`:

| Range | Purpose |
| --- | --- |
| .1 | Gateway |
| .2–.9 | Network infrastructure |
| .10–.49 | Servers / fixed infrastructure |
| .50–.99 | Reserved expansion |
| .100–.199 | Clients / dynamic systems |
| .200–.239 | Testing |
| .240–.254 | Reserved |

Examples:

| Address | Reserved role |
| --- | --- |
| 10.10.20.1 | Server gateway |
| 10.10.20.10 | Database |
| 10.10.20.20 | Application |
| 10.10.40.10 | SIEM |
| 10.10.40.20 | Vulnerability scanner |

This is an organizational standard, not a networking law. Hosts listed
below are logical reservations, not deployed systems.

## User Zone — 10.10.10.0/24

The User Zone contains representative employee endpoints.

Example systems may include:

- Windows user workstation
- Linux technical workstation
- Additional representative endpoints

User systems should be able to access authorized business services and
required internet resources.

User systems should not have unrestricted access to management or
security infrastructure.

Reserved examples (client range `.100–.199`):

| Host | Address |
| --- | --- |
| LBT-WIN-01 | 10.10.10.100 |
| LBT-LNX-01 | 10.10.10.101 |

## Server Zone — 10.10.20.0/24

The Server Zone contains systems providing Lazarus business and
infrastructure services.

Potential systems include:

- PostgreSQL company-state database
- Internal business applications
- APIs
- File/data services
- Supporting Linux services

Access should be restricted according to service requirements rather
than allowing unrestricted communication from all zones.

Reserved examples:

| Host | Address |
| --- | --- |
| LBT-DB-01 | 10.10.20.10 |
| LBT-APP-01 | 10.10.20.20 |
| LBT-FILE-01 | 10.10.20.30 |

These systems are not deployed yet.

## Management Zone — 10.10.30.0/24

The Management Zone is reserved for administrative functions and
management interfaces.

Potential uses include:

- Administrative workstation
- Infrastructure management
- Administrative interfaces
- Automation services

Normal employee endpoints should not have unrestricted access to the
Management Zone.

Administrative activity should be separately identifiable and logged.

Reserved example:

| Host | Address |
| --- | --- |
| LBT-ADMIN-01 | 10.10.30.10 |

Privileged administration should be distinguishable from normal employee
activity for IAM and detection engineering.

## Security Zone — 10.10.40.0/24

The Security Zone contains defensive security infrastructure.

Potential systems include:

- Wazuh
- Vulnerability scanner
- Security analytics services
- Log collectors
- Security management systems

Security systems may require controlled visibility into multiple
Lazarus zones.

Access from normal user networks to security management interfaces
should be restricted.

Reserved examples:

| Host | Address |
| --- | --- |
| LBT-SIEM-01 | 10.10.40.10 |
| LBT-VULN-01 | 10.10.40.20 |

Wazuh may receive telemetry from users, servers, identity, applications,
and network sources. That does not imply that every system may initiate
arbitrary connections back into the Security Zone. Firewall policy will
be defined during implementation.

## Cyber Range — 10.10.50.0/24

The Cyber Range is reserved for controlled security testing and
intentionally vulnerable systems.

The range may contain:

- Security testing workstation
- Intentionally vulnerable Linux systems
- Intentionally vulnerable Windows systems
- Disposable application targets
- Attack-simulation infrastructure

The Cyber Range must not have unrestricted access to the Lazarus
enterprise environment.

Aggressive or destructive testing must remain inside systems explicitly
authorized for that purpose.

```
              ENTERPRISE

Users ── Servers ── Security
               │
          RESTRICTED
               │
         ┌─────▼─────┐
         │ CYBER     │
         │ RANGE     │
         │           │
         │ Kali      │
         │ Targets   │
         └───────────┘
```

No range hosts, Kali, or vulnerable targets are installed in this step.
The network is reserved.

## DMZ / Future Zone — 10.10.60.0/24

The DMZ network is reserved for future services requiring controlled
external accessibility.

No DMZ systems are required for V0.1.

The network is reserved to avoid future addressing redesign.

## Cloud Services

External cloud platforms such as Microsoft Entra ID and Azure exist
outside Lazarus private laboratory address space. They are not another
`10.10.x.0/24` subnet.

```
                   INTERNET
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
   MICROSOFT CLOUD              LAB EDGE
                                 │
                        Lazarus networks
```

Communication with cloud services crosses an external trust boundary
and should use authenticated and encrypted connections.

Cloud resources must not be treated as implicitly trusted merely because
they belong to the Lazarus environment.

## Connectivity Principles

Allow what is required rather than allow everything and block a few
things.

| Source | Destination | Default |
| --- | --- | --- |
| Users | Internet | Controlled allow |
| Users | Business apps | Allow required services |
| Users | Database directly | Deny |
| Users | Management | Deny |
| Users | Security management | Deny |
| Apps | Database | Allow required DB connection |
| Security | Monitored systems | Controlled |
| Admin | Managed systems | Controlled |
| Cyber Range | Enterprise | Deny by default |
| Cyber Range | Internet | Restricted / controlled |

### NET-P01 — Default Restriction

Inter-zone communication should be limited to documented requirements.

### NET-P02 — User Isolation

User endpoints must not receive unrestricted access to management or
security infrastructure.

### NET-P03 — Database Isolation

End-user systems should not directly access backend databases unless a
specific requirement exists.

### NET-P04 — Security Visibility

Security infrastructure may receive telemetry from multiple zones while
management access remains restricted.

### NET-P05 — Administrative Separation

Administrative traffic should be distinguishable from normal employee
traffic.

### NET-P06 — Cyber Range Isolation

The Cyber Range must be denied unrestricted access to production-like
Lazarus networks.

### NET-P07 — Minimal Exposure

Internet-facing services should be minimized.

### NET-P08 — Documented Exceptions

Required cross-zone communication should be explicitly documented.

A later investigation example: `10.10.10.100` to `10.10.20.10:5432` is a
User Zone host connecting directly to PostgreSQL. Expected application
flow is workstation → application (HTTPS) → database (PostgreSQL), with
telemetry from each system to the SIEM.

## Lab Edge and Inter-Zone Routing

Lab edge / routing sits between the internet and Lazarus zones.

The product that performs routing and firewalling between these networks
is intentionally undecided. Candidates include hypervisor networking, a
virtual firewall/router, or a combination.

That choice depends on host and virtualization capabilities and is
deferred to Phase 2.01 Host Assessment.

Architecture defines the requirement now; implementation chooses the
product later.

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Logical architecture](logical-architecture.md)
- [Network architecture diagram v0.1](diagrams/network-architecture-v0.1.md)
- [ADR-001 Local-first infrastructure](../decisions/ADR-001-local-first.md)
