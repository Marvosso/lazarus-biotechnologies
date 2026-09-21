# Lazarus Biotechnologies Security Architecture

**Document ID:** LBT-ARCH-SEC-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer.

## Purpose

This document defines the security architecture used to protect the
Lazarus Biotechnologies virtual enterprise.

Security controls are derived from business requirements, information
classification, crown jewels, trust boundaries, identity architecture,
network architecture, and enterprise data flows.

The architecture follows defense-in-depth principles and includes
preventive, detective, and corrective controls.

Technology is selected after the required control is identified. The
existence of this document does not mark Wazuh, MFA, segmentation, or
OpenVAS as implemented.

The v0.1 diagram is in
[diagrams/security-architecture-v0.1.md](diagrams/security-architecture-v0.1.md).

Control inventory: [security-controls.csv](../../data/governance/security-controls.csv).

Requirement-to-control mapping:
[control-traceability.md](control-traceability.md).

## Control Types

### Preventive

Attempts to stop something from happening. Examples: MFA, firewall
rules, RBAC, system hardening.

### Detective

Helps identify something happening or having happened. Examples: Wazuh
alert, authentication logs, vulnerability scan, access review.

### Corrective

Helps restore or improve the environment afterward. Examples: remove
excessive access, patch a vulnerability, restore a backup, reconfigure
a firewall.

Good security usually involves all three. If MFA fails to prevent
account misuse, telemetry might detect it, and response procedures
provide corrective action.

## Defense-in-Depth Model

Lazarus security must not depend upon any single technical control.

```
                 ┌─────────────────────┐
                 │     GOVERNANCE      │
                 │ Risk / Controls     │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │      IDENTITY       │
                 │ MFA / RBAC / JML    │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │      ENDPOINT       │
                 │ Hardening / Logs    │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │      NETWORK        │
                 │ Segmentation        │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │    APPLICATION      │
                 │ AuthZ / Logging     │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │        DATA         │
                 │ Access / Encryption │
                 └──────────┬──────────┘
                            │
                         CROWN
                         JEWELS
       OBSERVABILITY SURROUNDS ALL LAYERS
```

Security controls are distributed across:

1. Governance
2. Identity
3. Endpoint
4. Network
5. Application
6. Data
7. Infrastructure
8. Observability
9. Resilience

Failure of one control should not automatically result in compromise
of a high-value resource.

## Identity Security

### Preventive Controls

- Unique technical identities
- Role/group-based access
- Least privilege
- MFA where supported
- Privileged identity separation
- Controlled access provisioning
- Timely deprovisioning

### Detective Controls

- Authentication telemetry
- Failed-login monitoring
- Group-membership monitoring
- Privileged-role monitoring
- Access reviews
- HR-to-IAM reconciliation

### Corrective Controls

- Account disablement
- Session revocation where supported
- Entitlement removal
- Privilege reduction
- Identity lifecycle remediation

Reconciliation is security analytics, not only SIEM:

```
HR                IAM
│                  │
LBT-0049           LBT-0049
TERMINATED         ENABLED
│                  │
└────────┬─────────┘
         ▼
      MISMATCH
         ▼
       FINDING
```

That mismatch can be detected in SQL before it becomes a SIEM alert.

## Endpoint Security

### Preventive Controls

- Documented baseline configuration
- Host firewall
- Account separation
- Patch management
- Restricted administrative access
- Unnecessary-service reduction

### Detective Controls

- Operating-system security logs
- Authentication events
- Process/activity telemetry where appropriate
- Configuration assessment
- Vulnerability scanning

### Corrective Controls

- Patch installation
- Configuration remediation
- Account remediation
- Endpoint rebuild or recovery

A commercial EDR is not required to satisfy the V0.1 learning
objective.

## Network Security

### Preventive Controls

- Security-zone segmentation
- Inter-zone firewall policy
- Cyber Range isolation
- Restricted management access
- Minimal inbound internet exposure
- Restricted direct database connectivity

### Detective Controls

- Firewall logs
- Network telemetry where practical
- Unexpected connection detection
- Service exposure assessment

### Corrective Controls

- Firewall-rule modification
- Network isolation
- Service restriction
- Segmentation improvement

Expected application path:

```
USER
 │
 │ 443
 ▼
APP
 │
 │ DB service
 ▼
DATABASE
```

A direct `USER → DATABASE` connection is itself a signal that the
architecture may have been violated.

## Application Security

### Preventive Controls

- Authentication
- Server-side authorization
- Role-based functionality
- Input validation
- Secrets management
- Restricted backend access
- Secure transport

### Detective Controls

- Authentication logging
- Authorization-failure logging
- Application activity logging
- Error monitoring
- Administrative-change logging

### Corrective Controls

- Application configuration changes
- Permission remediation
- Secret rotation
- Code remediation
- Deployment rollback where supported

Hiding an ORION button from an unauthorized user is not security. The
application must reject the request even if someone manually calls the
endpoint.

## Data Security

### Preventive Controls

- Information classification
- Business ownership
- Access control
- Program authorization
- Encryption in transit
- Appropriate protection of sensitive stored data
- Public-data sanitization

### Detective Controls

- Resource-access logging
- Authorization failures
- Access reviews
- Data-flow analysis
- Unexpected access analysis

### Corrective Controls

- Access revocation
- Data relocation
- Permission correction
- Public-content removal where appropriate
- Control improvement

LBT-4 does not mean everyone authorized for every LBT-4 resource.
Domain and business need still matter.

## Infrastructure Security

### Preventive Controls

- Minimal required services
- Secure configuration baselines
- Patch management
- Administrative separation
- Controlled remote management
- Configuration versioning where practical

### Detective Controls

- Vulnerability scanning
- Configuration assessment
- System telemetry
- Service inventory
- Administrative activity logging

### Corrective Controls

- Patching
- Configuration remediation
- Service removal
- Credential rotation
- System rebuild

Greenbone/OpenVAS is the preferred later assessment platform. It is
planned, not implemented.

## Security Monitoring Architecture

```
             TELEMETRY SOURCES
 Entra ──────────────────┐
                         │
 Windows ────────────────┤
                         │
 Linux ──────────────────┤
                         │
 Applications ───────────┼────► WAZUH
                         │         │
 Database ───────────────┤         ├── Search
                         │         ├── Rules
 Network ────────────────┤         ├── Alerts
                         │         └── Dashboards
 Security Tools ─────────┘
                                   │
                                   ▼
                              Alex Carter
                                   │
                                   ▼
                              Investigation
```

Wazuh is the preferred persistent local security monitoring platform.

The monitoring architecture should eventually ingest or correlate
telemetry from:

- Windows systems
- Linux systems
- Applications
- Identity systems where practical
- Databases where appropriate
- Network infrastructure
- Vulnerability-management systems

Microsoft Sentinel may later be used for targeted Azure and KQL
exercises but is not required as the persistent V0.1 SIEM.

## Telemetry Health

Logging infrastructure is itself a security control and must be
monitored accordingly.

The absence of expected telemetry may represent a security or
operational condition.

Future monitoring should support identification of:

- Endpoint telemetry loss
- Application logging failure
- Log-source interruption
- Collection failure
- Unexpected logging-volume changes

Example: `LBT-APP-01` dropping from ~850 events/hour to 0 is not “no
alerts.” It is a disappearance that must be investigated.

## Vulnerability Management Architecture

The vulnerability-management lifecycle is:

```
Asset Identification
        ↓
Authorized Assessment
        ↓
Finding
        ↓
Validation
        ↓
Business Context
        ↓
Prioritization
        ↓
Remediation
        ↓
Retesting
        ↓
Closure
```

This is not scan → export PDF → forget about it.

A later finding should carry business context, for example:

```
Finding: VULN-0042
Severity: High
Asset: LBT-APP-01
Owner: Engineering
Program: ORION
Classification: LBT-4
Crown Jewel Relationship: Federal Program Data
Status: Remediation Required
```

## Administrative Security

The project distinguishes between:

### Lab Owner Authority

Out-of-band authority required to build and maintain the virtual
environment.

### Simulated Enterprise Authority

Permissions granted to modeled Lazarus identities according to their
business roles.

Lab-owner capability must not be interpreted as authorization belonging
to the fictional Security Analyst persona.

Administrative activity used during simulations should follow the
simulated enterprise authorization model where practical.

## Resilience and Recovery

Security architecture must account for recovery as well as prevention.

Important components should have defined recovery approaches.

Potential mechanisms include:

- Version-controlled configuration
- Database backups
- VM snapshots where appropriate
- Rebuild documentation
- Container definitions
- Configuration exports

Snapshots must not substitute for appropriate backups of important
persistent data.

## Crown-Jewel Defense

Security prioritization protects business value, not only computers.
The following protection targets refine how Phase 0 crown jewels are
defended in this architecture:

| Crown Jewel | Primary Controls |
| --- | --- |
| CJ-01 Identity Infrastructure | MFA, privileged separation, identity telemetry, lifecycle controls |
| CJ-02 Federal Program Data | Program authorization, segmentation, access logging, classification |
| CJ-03 Proprietary Research | RBAC, data ownership, access logging, classification |
| CJ-04 Source Code & Engineering | Identity controls, repository authorization, secrets protection |
| CJ-05 Security Infrastructure | Restricted management, admin separation, monitoring |
| CJ-06 Corporate Sensitive Data | RBAC, ownership, classification, controlled access |

## Control Status Discipline

A control is not implemented because it is documented.

| Example | Status |
| --- | --- |
| Information classification | Implemented |
| Data ownership model | Implemented |
| MFA | Planned |
| Wazuh | Planned |
| Network segmentation | Planned |
| OpenVAS | Planned |

Later status values may include Planned, Implemented, Verified,
Partially Implemented, Failed, Retired, and Superseded.

## Control Failure Example — LBT-AC-003

If least privilege fails, Emily Davis might receive legitimate ORION
access plus unnecessary ATLAS and Cloud Admin entitlements.

Defense in depth does not rely on least privilege alone. Access
review, privileged-activity telemetry, or HR/IAM analytics may still
reveal the problem. Corrective action removes the access, determines
why it happened, and improves provisioning.

Ground truth for such scenarios remains separate from analyst-facing
evidence.

## ORION Flow Validation

Controls should exist at every stage of DF-004:

```
Emily
 │
 ├── Active employment
 ├── Active ORION assignment
 │
 ▼
Identity
 │
 ├── Unique account
 ├── MFA
 ├── Group authorization
 │
 ▼
Endpoint
 │
 ├── Security baseline
 ├── Host firewall
 ├── Logging
 │
 ▼
Network
 │
 ├── Segmentation
 ├── Required service only
 │
 ▼
ORION Application
 │
 ├── Authentication
 ├── Server-side authorization
 ├── Logging
 │
 ▼
LBT-4 Data
 │
 ├── Classification
 ├── Ownership
 ├── Restricted access
 └── Access telemetry
```

Surrounding all of it:

```
               WAZUH
                 │
                 ▼
             DETECTION
                 │
                 ▼
          INVESTIGATION
                 │
                 ▼
           REMEDIATION
```

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Logical architecture](logical-architecture.md)
- [Network architecture](network-architecture.md)
- [Identity architecture](identity-architecture.md)
- [Data flow architecture](data-flow-architecture.md)
- [Control traceability](control-traceability.md)
- [Crown jewels](../02-information-governance/crown-jewels.md)
- [ADR-001 Local-first](../decisions/ADR-001-local-first.md)
- [ADR-002 Identity authority](../decisions/ADR-002-identity-authority.md)
