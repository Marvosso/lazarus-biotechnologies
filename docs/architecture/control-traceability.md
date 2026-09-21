# Lazarus Biotechnologies Control Traceability

**Document ID:** LBT-ARCH-CTRL-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. Controls listed here apply to a simulated enterprise. No actual classified information, CUI, patient information, government data, or customer data is used.

## Purpose

Map business and technical requirements to architecture and security
controls so implementation can be traced:

```
BUSINESS REQUIREMENT
        ↓
TECHNICAL REQUIREMENT
        ↓
ARCHITECTURE
        ↓
SECURITY CONTROL
        ↓
IMPLEMENTATION
        ↓
TEST
        ↓
EVIDENCE
```

Control definitions live in
[security-controls.csv](../../data/governance/security-controls.csv).

A documented control is not an implemented control unless status says
so.

## Initial Traceability

| Requirement | Architecture | Control |
| --- | --- | --- |
| ID-001 Unique Identity | Identity Architecture | LBT-AC-001 |
| ID-005 Role-Based Access | Identity Architecture | LBT-AC-002 |
| ID-006 Least Privilege | Identity Architecture | LBT-AC-003 |
| ID-008 Authentication Controls | Identity Architecture | LBT-IA-001 |
| ID-010 Access Review | Identity Architecture | LBT-AC-004 |
| NET-004 Segmentation | Network Architecture | LBT-NET-001 |
| NET-005 Range Isolation | Network Architecture | LBT-NET-002 |
| LOG-001 Centralized Telemetry | Security Architecture | LBT-LOG-001 |
| LOG-002 Authentication Visibility | Security Architecture | LBT-LOG-002 |
| LOG-003 Endpoint Visibility | Security Architecture | LBT-LOG-001 |
| DATA-004 Classification | Information Governance | LBT-DP-001 |
| DATA-005 Ownership | Information Governance | LBT-DP-002 |
| SEC-003 Vulnerability Management | Security Architecture | LBT-VM-001 |
| SEC-007 Incident Response | Security Architecture | LBT-IR-001 |
| RES-001 Recovery | Security Architecture | LBT-RS-001 |
| CON-001 Recurring Cost Target | ADR-001 / Security Architecture | Persistent SIEM remains local (Wazuh); Sentinel is exercise-only |

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Security architecture](security-architecture.md)
- [Identity architecture](identity-architecture.md)
- [Network architecture](network-architecture.md)
