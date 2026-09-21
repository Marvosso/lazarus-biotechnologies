# Lazarus Biotechnologies Architecture Baseline

**Document ID:** LBT-ARCH-BASE-001  
**Architecture Version:** 0.1  
**Status:** Approved for Initial Implementation  
**Phase:** 1 — Enterprise Architecture  
**Baseline Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer.

## Purpose

This document establishes the first approved architecture baseline for
the Lazarus Biotechnologies virtual enterprise.

Architecture v0.1 represents the intended design prior to infrastructure
deployment.

Implementation may reveal technical, financial, operational, or security
constraints requiring architectural changes.

Material changes to the baseline must be documented through the project's
change and Architecture Decision Record process.

This is not a claim that the architecture is permanent. It is the
approved design we will attempt to build. Meaningful deviation must be
intentional and documented:

```
Architecture v0.1
        ↓
Implementation discovered constraint
        ↓
ADR
        ↓
Architecture v0.2
```

Approved architecture is not implemented architecture. Preferred
technologies listed below are not deployed.

## Baseline Components

Architecture v0.1 consists of the following authoritative documents:

| Component | Document |
| --- | --- |
| Enterprise Requirements | [enterprise-requirements.md](enterprise-requirements.md) |
| Logical Architecture | [logical-architecture.md](logical-architecture.md) |
| Network Architecture | [network-architecture.md](network-architecture.md) |
| Identity Architecture | [identity-architecture.md](identity-architecture.md) |
| Data Flow Architecture | [data-flow-architecture.md](data-flow-architecture.md) |
| Security Architecture | [security-architecture.md](security-architecture.md) |
| Control Traceability | [control-traceability.md](control-traceability.md) |

Supporting diagrams are maintained under `docs/architecture/diagrams/`.

Inventory: [architecture-inventory.csv](../../data/governance/architecture-inventory.csv).

Decision: [ADR-003](../decisions/ADR-003-architecture-baseline-v0.1.md).

## Technology Baseline

| Capability | Current Direction | State |
| --- | --- | --- |
| Company State | PostgreSQL | Preferred |
| Cloud Identity | Microsoft Entra ID | Preferred |
| Security Monitoring | Wazuh | Preferred |
| Vulnerability Management | Greenbone/OpenVAS | Preferred |
| Automation | Python / PowerShell | Preferred |
| Containers | Docker-compatible platform | Planned |
| Analytics | SQL / Power BI Desktop | Planned |
| Cloud Security Exercises | Azure / Microsoft Sentinel | Deferred |
| AI Employee Simulation | Undetermined | Deferred |

Technology marked "Preferred" remains subject to validation during
implementation.

No technology should be described as deployed until implementation and
verification have occurred.

Snapshot 001 lists these technologies as the intended stack. That listing
does not mean hands-on implementation has happened.

## Network Baseline

| Zone | Network | Purpose |
| --- | --- | --- |
| User | 10.10.10.0/24 | Employee endpoints |
| Server | 10.10.20.0/24 | Applications and data services |
| Management | 10.10.30.0/24 | Administrative systems |
| Security | 10.10.40.0/24 | Defensive security infrastructure |
| Cyber Range | 10.10.50.0/24 | Controlled security testing |
| DMZ / Future | 10.10.60.0/24 | Future externally accessible services |

Parent allocation: `10.10.0.0/16`

These addresses are the v0.1 planned network standard. Later changes
must be documented.

## Identity Baseline

The following identity principles are approved:

1. Company-state/HR information is authoritative for business identity.
2. Technical identity is separate from business identity.
3. Program assignments are separate from organizational roles.
4. Group- and role-based authorization is preferred over direct grants.
5. Least privilege is the default access principle.
6. Privileged activity must be distinguishable from routine activity.
7. Joiner, mover, and leaver events must affect technical access.
8. Sensitive access must eventually support periodic review.
9. Identity activity should produce security telemetry.
10. Modeled employees do not all require live cloud identities.

## Information Baseline

Lazarus uses the following internal information classification model:

- LBT-1 PUBLIC
- LBT-2 INTERNAL
- LBT-3 CONFIDENTIAL
- LBT-4 CONTROLLED

LBT-4 is an internal project classification and does not redefine or
replace official government CUI categories or markings.

All government-related, research, biomedical, employee, financial, and
business data used by the project must be synthetic.

Any artifact representing simulated CUI must clearly state:

`SIMULATED TRAINING DATA — NOT ACTUAL CUI`

## Security Baseline

Architecture v0.1 adopts defense in depth across:

- Governance
- Identity
- Endpoint
- Network
- Application
- Data
- Infrastructure
- Observability
- Resilience

Security controls may be:

- Preventive
- Detective
- Corrective

Security-control implementation status must distinguish between:

- Planned
- Implemented
- Verified

Future statuses may include:

- Partially Implemented
- Failed
- Retired
- Superseded

## Simulation Baseline

Lazarus represents a 50-person organization without requiring 50
physical or virtual endpoints.

The project will prioritize:

- Real security telemetry where practical
- Simulated organizational scale
- Persistent business state
- Representative infrastructure
- Deterministic and probabilistic simulation before AI-based simulation

Initial deployment will not intentionally introduce security failures
solely to manufacture findings.

Security failures and adversarial scenarios will be introduced during
later controlled phases.

## Architecture Consistency Review

The following scenarios were checked against Architecture v0.1 before
approval. No conceptual contradiction blocks implementation.

### Scenario A — New employee

HR → Company State → Technical Identity → Groups → Endpoint/Application → Telemetry → SIEM

**Pass.**

### Scenario B — ORION access

Employee → Active ORION Assignment → Program Entitlement → User Endpoint → ORION Application → LBT-4 Data → Telemetry

**Pass.**

### Scenario C — Employee leaves ORION but stays at Lazarus

Employment = ACTIVE; ORION assignment = EXPIRED → ORION entitlement removed → corporate identity remains active

**Pass.**

### Scenario D — Security analyst investigates

Wazuh → Alert → Alex Carter → Identity + Asset + Business Context → Investigation → Remediation → Persistent State Change

**Pass.**

### Scenario E — Controlled attack

Cyber Range is restricted from the enterprise except when interaction is
explicitly designed.

**Pass.**

### Scenario F — Portfolio publishing

Internal Evidence → Sanitization → Public Evidence → Portfolio

**Pass.**

## Open Architecture Decisions

The following decisions remain intentionally unresolved.

### OPEN-001 — Virtualization Platform

Decision depends on host operating system, hardware, virtualization
support, and available resources.

Target resolution: Phase 2.02

### OPEN-002 — Inter-Zone Routing and Firewall

Potential approaches include hypervisor-native networking, a virtual
firewall/router, or a combination.

Target resolution: Phase 2.03

### OPEN-003 — Initial VM and Container Allocation

Exact system placement depends on available CPU, memory, and storage.

Target resolution: Phase 2.01–2.06

### OPEN-004 — Entra Licensing and Live Identity Count

The number and capabilities of live cloud identities will depend on
available free or low-cost options at implementation time.

Target resolution: Phase 4

### OPEN-005 — Business Application Implementation

The internal business application's final framework and deployment model
have not yet been selected.

Target resolution: Phase 3.06

### OPEN-006 — Telemetry Integration Methods

Exact collection mechanisms will depend on the implemented platforms and
available integrations.

Target resolution: Phase 6

### OPEN-007 — Backup Implementation

Recovery requirements are defined, but exact backup technologies and
retention periods remain undecided.

Target resolution: Phase 2 / Phase 3

## Assumptions

Architecture v0.1 assumes:

1. A Windows-based physical host is available.
2. The host supports hardware virtualization.
3. Sufficient local storage exists for a small multi-system lab.
4. Internet connectivity is available when cloud services are required.
5. The project remains primarily single-host during initial deployment.
6. Only representative systems require continuous operation.
7. Synthetic data is sufficient for project objectives.
8. Free and open-source technologies remain preferred.
9. Recurring operating cost remains targeted at $0/month.
10. Cloud resources may be temporary rather than persistent.

Assumptions 2 and 3 will be tested in 02.01 Host Assessment. If the
machine cannot support the design, Architecture v0.1 will be adapted
rather than forcing the host to fit the design.
