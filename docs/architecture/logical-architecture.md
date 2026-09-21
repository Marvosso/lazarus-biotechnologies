# Lazarus Biotechnologies Logical Architecture

**Document ID:** LBT-ARCH-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer.

## Purpose

This document defines the logical technology architecture required to
support Lazarus Biotechnologies business operations and cybersecurity
learning objectives.

The logical architecture describes system responsibilities and
relationships without defining final physical deployment details.

Physical hostnames, RAM, and IP addresses are deferred to later
architecture and infrastructure steps. This document answers:

What systems and logical components need to exist to satisfy the
requirements in [enterprise-requirements.md](enterprise-requirements.md)?

Security is not a box sitting off to the side. It crosses every layer.

## Logical Layers

```
┌──────────────────────────────────────────────┐
│                 BUSINESS                     │
│ Employees │ Departments │ Programs │ Data    │
├──────────────────────────────────────────────┤
│                 IDENTITY                     │
│ HR Source │ Accounts │ Groups │ RBAC │ MFA   │
├──────────────────────────────────────────────┤
│              APPLICATIONS                    │
│ Portal │ Research │ Engineering │ Programs   │
├──────────────────────────────────────────────┤
│              INFRASTRUCTURE                  │
│ Windows │ Linux │ Containers │ Database      │
├──────────────────────────────────────────────┤
│              OBSERVABILITY                   │
│ Logs │ SIEM │ Detection │ Vulnerability Mgmt │
├──────────────────────────────────────────────┤
│                GOVERNANCE                    │
│ Assets │ Risk │ Controls │ Evidence │ Metrics│
└──────────────────────────────────────────────┘
```

The v0.1 component view is in
[diagrams/logical-architecture-v0.1.md](diagrams/logical-architecture-v0.1.md).

## Four Distinctions

These four things must stay separate:

| Concept | Question it answers | Example |
| --- | --- | --- |
| Company state | Who is this person in the business? | Maya's department and program |
| Identity | What account authenticates, and with what roles? | Maya's Entra account and groups |
| Business activity | What did they actually do? | Portal use, data access, engineering work |
| Security telemetry | What can the analyst observe? | Auth, endpoint, application, and system logs |

## Company State Layer

The Company State Layer represents authoritative structured information
about the fictional organization.

Initial responsibilities include:

- Employees
- Departments
- Reporting relationships
- Employment status
- Program assignments
- Information authorization
- Asset relationships

PostgreSQL is the current preferred datastore.

Company state is distinct from generated security telemetry.

PostgreSQL is preferred because it supports SQL, relational modeling,
Python integration, APIs, Power BI, security analytics, and IAM
correlation at $0 recurring cost.

Example later analysis: program assignment ended, access not removed.

```sql
SELECT
    e.employee_id,
    e.first_name,
    e.last_name,
    p.program_name
FROM employees e
JOIN program_assignments pa
    ON e.employee_id = pa.employee_id
JOIN programs p
    ON pa.program_id = p.program_id
WHERE pa.end_date < CURRENT_DATE
AND pa.access_removed = FALSE;
```

If investigation or remediation changes access, company state should
change and persist. Lazarus does not reset after every exercise.

## Identity Layer

The Identity Layer provides technical identities and authorization
relationships for Lazarus personnel.

Responsibilities include:

- User identities
- Authentication
- Group membership
- Role-based authorization
- Administrative identities
- MFA
- Identity lifecycle events

Microsoft Entra ID is the preferred cloud identity platform where
available.

The Company State Layer remains the business source of truth for
employee information.

These are not the same thing:

```
PostgreSQL
"Alex Carter works for Lazarus."

        ↓

Entra
"alex.carter can authenticate."

        ↓

Authorization
"Alex Carter belongs to Security-Analysts."

        ↓

Application
"Security-Analysts may access security dashboard."
```

## Business Services Layer

Business services provide resources that employees interact with during
normal simulated operations.

The environment does not require a large commercial application stack.
A small representative business environment is sufficient.

Initial logical service categories include:

### Corporate Services

Representative HR, corporate, and administrative resources.

### Research Services

Synthetic biomedical research information and workflows.

### Engineering Services

Representative development resources and technical workflows.

### Federal Program Services

Program-specific resources for ORION, ATLAS, and HORIZON.

### Internal Portal

A lightweight internal application may provide common business
workflows and generate attributable application telemetry.

Different users should see different resources. One internal application
can later support directory, programs, documents, research, IT support,
security, and approvals without becoming five separate fake SaaS products.

## Simulation Layer

The Simulation Layer generates routine business activity using the
modeled Lazarus workforce.

Responsibilities will eventually include:

- Work schedules
- Authentication behavior
- Application interaction
- Data access
- Engineering activity
- Program activity
- Employee lifecycle events

The simulation engine must distinguish simulated business state from
security telemetry.

Initial simulation should use deterministic and probabilistic logic.

AI-driven employee behavior is deferred to a later phase.

Conceptually:

```
if employee.department == "Engineering":
    perform_engineering_activity()

if employee.program == "ATLAS":
    access_atlas_resources()
```

## Endpoint Layer

Representative endpoints provide real operating-system behavior and
security telemetry.

The environment will use a small number of systems representing multiple
employee personas rather than one endpoint per modeled employee.

Initial endpoint categories:

- Windows user endpoint
- Linux technical endpoint
- Administrative environment where justified

Endpoint activity should be attributable to modeled Lazarus identities
where practical.

A single Windows endpoint may represent different employees at different
scheduled periods, producing real login, application, and data-access
telemetry under those identities.

## Observability Layer

The Observability Layer provides centralized visibility into activity
occurring throughout the Lazarus environment.

Telemetry sources may include:

- Identity
- Authentication
- Windows
- Linux
- Applications
- Databases
- Network infrastructure
- Vulnerability systems

Wazuh is the current preferred local security monitoring platform.

Selected telemetry may later be sent to Microsoft Sentinel during
controlled cloud-security exercises.

```
                       WAZUH

Windows ───────────────┐
Linux ─────────────────┤
Application ───────────┤
Authentication ────────┼──► Search / Detection / Investigation
Network ───────────────┤
Security tools ────────┘
```

The security analyst persona (Alex Carter) investigates and remediates
using observable evidence. Remediation should write back into company
state so the enterprise is actually different afterward.

## Vulnerability Management

The Vulnerability Management function identifies and tracks technical
weaknesses affecting authorized Lazarus systems.

Responsibilities include:

- Asset discovery
- Vulnerability scanning
- Finding validation
- Risk prioritization
- Remediation tracking
- Retesting
- Metrics

Greenbone/OpenVAS is the preferred initial free vulnerability scanning
platform.

Technical severity should eventually be combined with asset and business
context. A CVSS score is not sufficient by itself:

```
Vulnerability
     │
     ▼
WEB-02
     │
     ▼
ORION service
     │
     ▼
LBT-4 data
     │
     ▼
Federal Program Crown Jewel
```

## Governance and Analytics Layer

Security and business information should eventually support governance,
risk, compliance, and analytical workflows.

Capabilities may include:

- Asset inventory
- Risk register
- Control evidence
- Access reviews
- Vulnerability metrics
- Incident metrics
- Security maturity tracking
- SQL analysis
- Power BI dashboards

This layer consumes information from operational systems rather than
replacing them.

```
PostgreSQL ────────────┐
IAM exports ───────────┤
Assets ────────────────┤
Vulnerabilities ───────┼──► Power BI
Incidents ─────────────┤
Risk register ─────────┤
Controls ──────────────┘
```

## Trust Boundaries

A trust boundary is a place where data or activity moves between systems
with different levels of trust or control.

Initial boundaries:

```
                  INTERNET
                     │
             TRUST BOUNDARY #1
                     │
                     ▼
              CLOUD SERVICES
                Entra etc.
                     │
             TRUST BOUNDARY #2
                     │
                     ▼
              LAZARUS LAB
                     │
       ┌─────────────┼─────────────┐
       │             │             │
    Endpoints     Servers       Security
       │             │             │
       └─────────────┼─────────────┘
                     │
             TRUST BOUNDARY #3
                     │
                     ▼
                CYBER RANGE
```

These boundaries will be made more precise in 01.03 Network Architecture.

## Architecture Principles

### AP-001 — Business Before Technology

Technology must support an identified business, security, or educational
requirement.

### AP-002 — Local First

Persistent workloads should run locally where practical.

### AP-003 — Real Telemetry

Real system telemetry should be preferred over fabricated log records
where practical.

### AP-004 — Simulated Scale

Organizational scale may be simulated without reproducing equivalent
physical infrastructure.

### AP-005 — Persistent State

Business and security state should persist so actions and remediation
have future consequences.

### AP-006 — Least Privilege

Access should be minimized according to legitimate business need.

### AP-007 — Observable by Design

Systems should be designed with appropriate telemetry rather than
logging being added only after deployment.

### AP-008 — Reproducibility

Important systems and configurations should be reproducible.

### AP-009 — Evidence by Design

Implementations should produce evidence capable of demonstrating the
skill or result achieved.

### AP-010 — Cost Awareness

Architecture decisions must consider recurring operating cost.

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Logical architecture diagram v0.1](diagrams/logical-architecture-v0.1.md)
- [ADR-001 Local-first infrastructure](../decisions/ADR-001-local-first.md)
