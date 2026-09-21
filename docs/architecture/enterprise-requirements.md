# Lazarus Biotechnologies Enterprise Requirements

**Document ID:** LBT-ARCH-REQ-001  
**Status:** Draft  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-10

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used.

---

## 1. Purpose

This document translates Lazarus Biotechnologies business operations,
information requirements, workforce structure, and security objectives
into technical requirements.

Technology selections will be made only after requirements have been
defined and reviewed.

Every major technology choice should trace back to a business or
security requirement in this document.

---

## 2. Requirement Categories

Requirements are grouped into:

- Business
- Identity
- Endpoint
- Application
- Data
- Infrastructure
- Network
- Security
- Logging and Monitoring
- Resilience
- Governance
- Cost and Operational Constraints

---

## 3. Business Requirements

### BR-001 — Hybrid Workforce

The environment must support users working from both office-style and
remote locations.

### BR-002 — Departmental Separation

Users must be associated with their organizational department and team.

### BR-003 — Program Assignments

Employees may participate in federal programs independently of their
organizational department.

Program assignments must therefore be represented separately from job
roles.

Department membership is not equivalent to program assignment. A
software engineer may belong to Engineering while assigned to ATLAS.

### BR-004 — Employee Lifecycle

The environment must support hires, transfers, promotions, program
changes, and terminations.

### BR-005 — Business Applications

Users must be able to interact with representative business services
sufficient to generate realistic enterprise activity.

### BR-006 — Research Operations

Biomedical R&D users must have access to representative research data
and technical workflows.

### BR-007 — Engineering Operations

Engineering users must be able to interact with representative source
code, development systems, and technical resources.

### BR-008 — Federal Program Operations

Authorized users must be able to interact with synthetic program data
associated with ORION, ATLAS, and HORIZON.

### BR-009 — Growth

The architecture must support future company growth without requiring
a complete redesign.

---

## 4. Identity Requirements

### ID-001 — Unique Identity

Every active employee represented in an identity system must have a
unique technical identity.

### ID-002 — HR Source of Truth

Business identity attributes must originate from the Lazarus HR/company
state system.

### ID-003 — Organizational Attributes

Technical identities must be capable of representing:

- employee ID
- department
- title
- manager
- employment type
- employment status

### ID-004 — Program Membership

Technical access must support program-specific authorization independently
of department membership.

### ID-005 — Role-Based Access

Access should be assigned through roles or groups wherever practical
rather than individual user-by-user permissions.

### ID-006 — Least Privilege

Users should receive only the access necessary for their current business
responsibilities.

### ID-007 — Privileged Identity Separation

Administrative access should be distinguishable from normal employee
access.

### ID-008 — Authentication Controls

The environment should support secure authentication and MFA where
available.

### ID-009 — Joiner / Mover / Leaver

Identity provisioning, modification, and deprovisioning must support the
employee lifecycle.

### ID-010 — Access Review

The environment must eventually support periodic review of access
entitlements.

### ID-011 — Identity Telemetry

Authentication and identity events must be observable by the security
monitoring environment.

---

## 5. Endpoint Requirements

The environment uses a small number of real endpoints representing
employee personas. Organizational scale is modeled logically; it does
not require one physical system per employee.

### EP-001 — Representative Endpoints

The environment must contain a small number of real endpoints representing
different employee personas rather than one machine per modeled employee.

### EP-002 — Windows Endpoint

At least one representative Windows user system must exist.

### EP-003 — Linux Endpoint

At least one representative Linux technical system or workstation must
exist.

### EP-004 — User Attribution

Endpoint activity must be attributable to a modeled Lazarus user where
practical.

### EP-005 — Endpoint Logging

Representative endpoints must generate host and authentication telemetry.

### EP-006 — Endpoint Security Baseline

Endpoints should have documented initial security configurations.

### EP-007 — Controlled Vulnerability

Selected lab systems may later contain deliberately introduced weaknesses
for authorized security exercises.

### EP-008 — Recoverability

Important lab endpoints should be reproducible or recoverable after
failure or testing.

---

## 6. Application Requirements

### APP-001 — Internal Business Application

The environment must contain at least one internal application used by
multiple employee roles.

### APP-002 — Role-Aware Access

Applications should support different levels of access based on user or
business role where practical.

### APP-003 — Authentication Activity

Applications should produce observable authentication or session activity.

### APP-004 — Business Activity Logging

Applications should produce logs representing meaningful user activity.

### APP-005 — Synthetic Business Data

Applications must use synthetic data only.

### APP-006 — API Capability

At least one system should eventually expose an API that can be used by
the simulation engine.

### APP-007 — Extensibility

Applications should be designed so future workflows can be added without
rebuilding the enterprise architecture.

---

## 7. Data Requirements

### DATA-001 — Company State

A structured datastore must maintain authoritative company state.

### DATA-002 — Workforce Data

The system must store employees, departments, managers, employment
status, and employment type.

### DATA-003 — Program Data

Federal program membership must be represented separately from
organizational structure.

### DATA-004 — Information Classification

Data and resources must be capable of being associated with Lazarus
information classifications.

### DATA-005 — Ownership

Sensitive data must have an identifiable business owner.

### DATA-006 — Synthetic Data Only

No real government, patient, customer, or other protected data may be
used.

### DATA-007 — Historical State

Important business and security state changes should be historically
reconstructable.

### DATA-008 — Analytical Access

Structured project data should be suitable for later SQL and Power BI
analysis.

---

## 8. Infrastructure Requirements

### INF-001 — Local-First

Persistent compute should run locally where practical.

### INF-002 — Low Cost

The target recurring operating cost is $0 per month.

### INF-003 — Virtualization

The architecture must support multiple isolated virtual systems on a
single physical host.

### INF-004 — Linux Services

The environment must support Linux-based infrastructure and security
services.

### INF-005 — Windows Systems

The environment must support representative Windows workloads.

### INF-006 — Containers

Containerization should be supported for lightweight applications and
services where appropriate.

### INF-007 — Infrastructure Reproducibility

Important infrastructure configuration should be reproducible and
documented.

### INF-008 — Resource Efficiency

Systems should not need to remain powered on when they are not required
for a specific exercise or business simulation.

---

## 9. Network Requirements

### NET-001 — Isolated Lab Network

Lazarus systems must operate within controlled lab networking.

### NET-002 — Internet Access

Selected systems may access the internet where required for updates or
legitimate services.

### NET-003 — Inbound Exposure

Internet-facing services should be minimized.

### NET-004 — Segmentation

The architecture must support separation between systems of different
security purposes.

### NET-005 — Attack Range Isolation

Destructive or aggressive testing must occur in a separately controlled
environment.

### NET-006 — Network Visibility

The architecture should support collection of relevant network telemetry.

### NET-007 — Addressing Standard

Lazarus must use a documented internal addressing scheme.

---

## 10. Security Requirements

### SEC-001 — Least Privilege

Access must follow least-privilege principles.

### SEC-002 — Defense in Depth

Security should not depend on a single control.

### SEC-003 — Vulnerability Management

Systems must eventually be assessed for known vulnerabilities.

### SEC-004 — Secure Configuration

Important systems should have documented baseline configurations.

### SEC-005 — Security Testing

The project must support controlled testing of security controls.

### SEC-006 — Crown Jewel Awareness

Security prioritization must consider the business importance of affected
assets and data.

### SEC-007 — Incident Response

Security events must eventually support formal investigation and response.

### SEC-008 — Security Evolution

Security posture must be capable of improving or degrading over time.

### SEC-009 — Secrets Protection

Credentials, tokens, keys, and other secrets must not be stored in the
public repository.

---

## 11. Logging and Monitoring Requirements

### LOG-001 — Centralized Telemetry

Relevant security logs must be collected centrally.

### LOG-002 — Authentication Visibility

Successful and failed authentication events must be observable.

### LOG-003 — Endpoint Visibility

Representative host security activity must be observable.

### LOG-004 — Application Visibility

Important business application activity must be observable.

### LOG-005 — Administrative Visibility

Privileged or administrative activity should be distinguishable from
routine user activity.

### LOG-006 — User Attribution

Where practical, security events should identify the associated Lazarus
employee.

### LOG-007 — Asset Attribution

Security events should identify the affected asset.

### LOG-008 — Business Context

Security analysis should eventually be capable of associating technical
events with department, program, classification, and crown-jewel context.

### LOG-009 — Retention

Security telemetry must remain available long enough to support
investigations and exercises within reasonable local storage constraints.

### LOG-010 — Detection Capability

Collected telemetry must support creation and testing of custom security
detections.

---

## 12. Resilience Requirements

### RES-001 — Recovery

Critical project components must have a defined recovery method.

### RES-002 — Configuration Preservation

Important configurations must be backed by version-controlled
documentation or code where practical.

### RES-003 — Data Backup

Important Lazarus state data should have recoverable backups.

### RES-004 — Disposable Test Systems

Systems intended for destructive testing should be resettable or
rebuildable.

### RES-005 — Failure Simulation

Future project phases should support controlled service failures and
recovery exercises.

---

## 13. Governance Requirements

### GOV-001 — Asset Ownership

Important assets must have an assigned owner.

### GOV-002 — Data Ownership

Sensitive information must have an assigned business owner.

### GOV-003 — Change Documentation

Meaningful architectural and security changes must be documented.

### GOV-004 — Architecture Decisions

Major technical decisions must use Architecture Decision Records.

### GOV-005 — Evidence

Implemented security controls should eventually have supporting evidence.

### GOV-006 — Risk Management

Identified security risks must eventually be recorded and tracked.

### GOV-007 — Control Mapping

Selected implemented controls may later be mapped to public frameworks
such as NIST SP 800-171 for educational purposes.

### GOV-008 — Honest Representation

Portfolio material must clearly identify Lazarus as a simulated personal
project rather than professional employment.

---

## 14. Cost and Operational Constraints

### CON-001 — Recurring Cost Target

Recurring project operating cost should remain at $0 whenever practical.

### CON-002 — Soft Cost Ceiling

Recurring expenses above $10 per month require explicit justification.

### CON-003 — Open Source Preference

Open-source or free technologies should be preferred when they satisfy
the project requirement.

### CON-004 — Cloud Justification

Cloud services should be used where they provide meaningful technical
or educational value.

### CON-005 — Simulated Scale

Enterprise scale may be represented logically rather than through one
physical system per employee.

### CON-006 — Hardware Constraint

The architecture must operate within the capabilities of the available
physical lab host.

Host capacity is not yet measured. VM counts and concurrent workloads
will be designed after the Phase 2 host assessment.

---

## 15. Requirement Priorities

Requirements are prioritized as:

| Priority | Meaning |
| --- | --- |
| MUST | Required for V0.1 or for a hard project constraint |
| SHOULD | Important, but must not block V0.1 if a later phase can satisfy it |
| COULD | Valuable later; do not treat as a dependency for earlier phases |

Not every requirement is tagged in this draft. The following examples
establish how later architecture work should treat scope:

| Requirement | Priority |
| --- | --- |
| Centralized telemetry | MUST |
| Synthetic data only | MUST |
| Attack-range isolation | MUST |
| Windows endpoint | MUST |
| Linux endpoint | SHOULD |
| Network IDS | SHOULD |
| AI employee agents | COULD |
| Sentinel integration | COULD |

Work that is not necessary to satisfy V0.1 must not block progress.
