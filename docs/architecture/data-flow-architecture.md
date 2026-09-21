# Lazarus Biotechnologies Data Flow Architecture

**Document ID:** LBT-ARCH-DATA-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer. Any artifact representing simulated CUI must clearly state: SIMULATED TRAINING DATA — NOT ACTUAL CUI.

## Purpose

This document describes how business, identity, application, security,
and governance information moves through the Lazarus Biotechnologies
environment.

The purpose of data-flow analysis is to identify:

- Data sources
- Data destinations
- Trust boundaries
- Authorization requirements
- Sensitive information
- Security controls
- Logging requirements
- Potential exposure paths

Every time data moves between components, architecture should be able to
answer: who initiated it, what data moved, where it went, whether it was
authorized, whether it was protected, and whether it was logged.

The v0.1 diagram is in
[diagrams/data-flow-v0.1.md](diagrams/data-flow-v0.1.md).

## Data Domains

Classification is assigned to the information, not simply the
department.

### Corporate Data

Examples:

- Employee records
- Financial records
- Contracts
- Vendor information

Typical classification: LBT-2 through LBT-3

### Research Data

Examples:

- Synthetic research datasets
- Research results
- Models
- Proprietary research documentation

Typical classification: LBT-2 through LBT-4

### Engineering Data

Examples:

- Source code
- Architecture documentation
- CI/CD information
- Application configuration

Typical classification: LBT-2 through LBT-4

### Federal Program Data

Examples:

- ORION records
- ATLAS records
- HORIZON records
- Synthetic controlled program artifacts

Typical classification: LBT-3 through LBT-4

### Security Data

Examples:

- Logs
- Vulnerability findings
- Incident records
- Detection rules
- Architecture information
- Risk records

Typical classification: LBT-2 through LBT-4

## DF-001 — Employee Identity Creation

```
HR
 │
 │ Creates employee
 ▼
COMPANY STATE
PostgreSQL
 │
 ├── Employee ID
 ├── Name
 ├── Department
 ├── Manager
 ├── Employment status
 └── Employment type
 │
 ▼
IDENTITY PROVISIONING
 │
 ▼
TECHNICAL IDENTITY
```

### Source

Authorized HR function

### Data

Employee business identity information

### Destination

Company-state datastore

### Downstream Consumer

Identity lifecycle process

### Security Requirements

- HR information must be protected from unauthorized modification.
- Employee identifiers must remain unique.
- Employment status must originate from the authoritative business source.
- Identity creation must be traceable to an employee record.
- Provisioning activity should be auditable.

### Expected Telemetry

- Employee record creation
- Identity provisioning event
- Account creation
- Initial group assignment

A later portfolio artifact should be able to trace: employee created →
identity created → groups assigned → first authentication.

## DF-002 — User Authentication

```
Employee
   │
   ▼
Workstation
   │
   │ authentication
   ▼
Identity Provider
   │
   ├── success
   │
   └── failure
         │
         ▼
     Telemetry
         │
         ▼
       SIEM
```

### Source

Employee technical identity

### Components

- User endpoint
- Identity provider
- Target service
- Security monitoring platform

### Security Requirements

- Authentication must use approved identities.
- MFA should be used where supported and appropriate.
- Authentication events should identify the account and source.
- Administrative authentication should be distinguishable from normal use.
- Authentication telemetry should be centrally observable.

### Expected Telemetry

- Authentication success
- Authentication failure
- MFA activity
- Source device or address
- Target resource

## DF-003 — Business Application Access

```
Employee
   │
   ▼
USER ENDPOINT
10.10.10.x
   │
   │ HTTPS
   ▼
BUSINESS APPLICATION
10.10.20.x
   │
   │ controlled backend connection
   ▼
DATABASE
10.10.20.x
```

### Source

Authorized employee endpoint

### Destination

Lazarus business application

### Backend

Company-state or application datastore

### Security Requirements

- User authentication is required for protected resources.
- Application authorization must restrict available functionality.
- User endpoints should not require direct database access.
- Sensitive data should be protected in transit.
- Relevant application activity should be logged.
- Backend database access should be restricted to required application services.

### Expected Telemetry

- Authentication
- Session creation
- Resource access
- Authorization failures
- Application actions
- Backend service activity

## DF-004 — ORION Controlled Information Access

This is the first high-value data flow.

```
Emily Davis
LBT-0046
        │
        ▼
Technical Identity
        │
        ▼
Is ORION assignment active?
        │
       YES
        │
        ▼
ORION entitlement
        │
        ▼
LBT-WIN-01
User Zone
        │
        │ HTTPS
        ▼
ORION Resource
Server Zone
        │
        ▼
SIMULATED ORION DATA
LBT-4 CONTROLLED
```

### Actor

Authorized ORION program participant

### Example

Emily Davis — LBT-0046 — Program Analyst

### Information

Synthetic ORION program information classified LBT-4 CONTROLLED.

Any artifact representing simulated CUI must clearly state:

`SIMULATED TRAINING DATA — NOT ACTUAL CUI`

### Authorization Requirements

Access requires:

1. Active Lazarus employment
2. Active technical identity
3. Active ORION program assignment
4. Appropriate ORION entitlement
5. Legitimate business need

### Security Requirements

- Authentication required
- Authorization validated
- Encryption in transit
- Controlled application path
- Access logging
- Restricted backend access
- Appropriate storage protections
- Access revocation when assignment ends

### Expected Telemetry

- User authentication
- ORION application authentication
- Resource access
- Authorization failure
- Administrative changes

### Assignment expiry

If Emily's ORION assignment ends, expected state is:

| Record | State |
| --- | --- |
| HR employment | ACTIVE |
| Corporate identity | ACTIVE |
| ORION assignment | EXPIRED |
| ORION access | REMOVED |

Emily still works for Lazarus. The account is not disabled. The ORION
entitlement is removed while normal employee access is preserved. That
is identity governance, not only account management.

## DF-005 — Security Telemetry

```
ENDPOINTS ──────────┐
                    │
SERVERS ────────────┤
                    │
APPLICATIONS ───────┤
                    ├────► SECURITY TELEMETRY
IDENTITY ───────────┤             │
                    │             ▼
DATABASE ───────────┤           WAZUH
                    │             │
NETWORK ────────────┘             ▼
                              Alex Carter
```

### Sources

Security-relevant systems throughout the Lazarus environment.

Potential sources include:

- Windows
- Linux
- Applications
- Identity services
- Databases
- Network systems
- Vulnerability-management systems

### Destination

Centralized security monitoring platform.

### Security Requirements

- Telemetry should identify the originating system.
- User activity should be attributable where practical.
- Security telemetry should be protected against unauthorized modification.
- Access to centralized security telemetry should be restricted.
- Collection failure should eventually be detectable.

### Downstream Uses

- Detection
- Investigation
- Incident response
- Metrics
- Control validation
- Security analytics

A system that stops sending logs is itself a security event.

## DF-006 — Vulnerability Information

```
Vulnerability Scanner
       │
       │ authorized scan
       ▼
Lazarus Asset
       │
       ▼
Finding
       │
       ├── CVE
       ├── severity
       ├── affected service
       └── evidence
       │
       ▼
Asset Context
       │
       ├── owner
       ├── function
       ├── program
       ├── classification
       └── crown jewel?
       │
       ▼
Risk Prioritization
```

### Source

Authorized vulnerability scanner

### Target

Approved Lazarus assets

### Output

Technical vulnerability findings

### Context Enrichment

Findings should eventually be associated with:

- Asset
- Asset owner
- Business function
- Information classification
- Program
- Crown-jewel relationship
- Remediation status

### Security Requirements

- Scanning must be limited to authorized systems.
- Vulnerability findings must be protected from unnecessary exposure.
- Remediation status should be historically traceable.
- Retesting should validate remediation.

## DF-007 — Investigation and Remediation

This is the living-company feedback loop.

```
ALERT
  │
  ▼
ANALYST
  │
  ▼
INVESTIGATION
  │
  ├── identity
  ├── endpoint
  ├── application
  ├── network
  └── business context
  │
  ▼
FINDING
  │
  ▼
REMEDIATION
  │
  ▼
SYSTEM STATE CHANGES
  │
  ▼
NEW SECURITY POSTURE
```

Security investigations consume telemetry and business context.

Potential inputs include:

- Alerts
- Authentication events
- Endpoint activity
- Application activity
- Identity state
- Program assignments
- Asset context
- Vulnerability information

Investigation may result in changes to:

- Identity access
- System configuration
- Network policy
- Application configuration
- Security detections
- Governance records

Remediation should alter persistent Lazarus state where appropriate.

## DF-008 — Governance and Security Analytics

```
HR ────────────────┐
IAM ───────────────┤
Assets ────────────┤
Vulnerabilities ───┤
Incidents ─────────┼────► Analytics Dataset
Risks ─────────────┤              │
Controls ──────────┤              ▼
Telemetry ─────────┘          SQL / Power BI
                                  │
                                  ▼
                           Security Metrics
```

Structured business and security information may be transformed into
analytical datasets.

Potential sources include:

- Workforce state
- Identity state
- Access entitlements
- Asset inventory
- Vulnerabilities
- Incidents
- Risks
- Controls
- Security telemetry

Analytical datasets may be consumed through:

- SQL
- Python
- Power BI
- Future portfolio systems

Public portfolio datasets must pass through sanitization before
publication.

## Trust-Boundary Analysis

| Flow | Boundary crossed | Sensitivity | Primary concern |
| --- | --- | --- | --- |
| Employee → Entra | Internet/cloud | Identity | Credential theft |
| User → App | User → Server | LBT-2–4 | Unauthorized access |
| App → DB | Application → Data | LBT-2–4 | Data exposure |
| Systems → SIEM | Enterprise → Security | Security | Telemetry integrity |
| Scanner → Asset | Security → Enterprise | Security | Scan scope |
| Enterprise → Cyber Range | Enterprise → Untrusted/test | Variable | Isolation |
| Internal → Portfolio | Private → Public | Variable | Information disclosure |

Internal incident material must not be published directly:

```
Internal incident report
        │
        ❌
        │
DO NOT DIRECTLY PUBLISH
        │
        ▼
Sanitization
        │
        ▼
Public Case Study
```

## Data States

### Data at Rest

Information stored in:

- Databases
- Files
- Logs
- Backups
- Repositories

### Data in Transit

Information moving between systems or trust boundaries.

Sensitive traffic should use appropriate encrypted protocols where
supported.

### Data in Use

Information actively processed or displayed by applications, users, or
analytical systems.

Security controls must consider all three states rather than focusing
only on stored data.

Example: an ORION document stored in a database is at rest; sent over
HTTPS it is in transit; displayed to Emily it is in use. Encryption does
not replace authorization. Emily can have a perfectly encrypted
connection to something she should not be allowed to access.

## Logging Checkpoints

High-value business flows should contain sufficient telemetry to
reconstruct significant activity.

Where practical, evidence should exist for:

1. User authentication
2. Source endpoint
3. Application session
4. Authorization decision
5. Resource access
6. Administrative changes

For a normal ORION access:

```
Emily
  │
  ▼
[1] Endpoint          Windows event
  │
  ▼
[2] Authentication    Identity sign-in
  │
  ▼
[3] Application       App session
  │
  ▼
[4] Authorization     Access decision
  │
  ▼
[5] Data access       Resource-access event
```

Logging requirements will be finalized during security architecture.
These checkpoints are the V0.1 acceptance test for observable activity.

## Architecture Trace — Emily Davis / ORION

| Question | Answer |
| --- | --- |
| Who? | Emily Davis — LBT-0046 |
| Why? | Program Analyst assigned to ORION |
| Identity? | Active technical identity |
| Authorization? | Active ORION assignment + appropriate entitlement |
| From where? | Representative user endpoint `10.10.10.x` |
| To where? | ORION business service `10.10.20.x` |
| What data? | Synthetic ORION information, LBT-4 CONTROLLED |
| How? | Authenticated application session over encrypted transport |
| Direct database access? | No |
| What should be logged? | Authentication, source endpoint, application session, authorization, resource access |
| Where does security see it? | Centralized telemetry / Wazuh |
| What happens when ORION assignment expires? | Program entitlement removed while normal employee identity remains active |

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Logical architecture](logical-architecture.md)
- [Network architecture](network-architecture.md)
- [Identity architecture](identity-architecture.md)
- [Data flow diagram v0.1](diagrams/data-flow-v0.1.md)
- [Crown jewels](../02-information-governance/crown-jewels.md)
- [Information classification](../02-information-governance/information-classification.md)
