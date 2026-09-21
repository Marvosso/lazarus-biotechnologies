# Lazarus Biotechnologies Identity Architecture

**Document ID:** LBT-ARCH-IAM-001  
**Status:** Draft  
**Version:** 0.1  
**Phase:** 1 — Enterprise Architecture  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. All employees, organizations, government programs, research data, controlled information, incidents, and business activity in this project are synthetic and exist only for cybersecurity education and portfolio development. No actual classified information, CUI, patient information, government data, or customer data is used. Lazarus Biotechnologies is not an employer.

## Purpose

This document defines the identity and access management architecture
for the Lazarus Biotechnologies virtual enterprise.

The architecture separates business identity, technical identity,
authorization, and access entitlements so that employee lifecycle and
access-control failures can be modeled and investigated independently.

IAM is an enterprise process, not only user creation in Entra:

```
HR says who you are
        ↓
IAM creates your identity
        ↓
Business role determines baseline access
        ↓
Program assignments add scoped access
        ↓
Applications enforce authorization
        ↓
Logs prove what happened
        ↓
Access reviews verify it still makes sense
```

Day 0 is a clean, reasonably designed least-privilege environment. Orphaned
accounts, excessive privileges, and stale access are future scenarios, not
initial design.

The v0.1 relationship diagram is in
[diagrams/identity-architecture-v0.1.md](diagrams/identity-architecture-v0.1.md).

Related decision: [ADR-002 Identity authority](../decisions/ADR-002-identity-authority.md).

## Five Concepts

These must not be collapsed into one field.

| Concept | Meaning | Example |
| --- | --- | --- |
| Business identity | Who the person is in the company | Alex Carter, employee LBT-0018, Security Analyst |
| Technical identity | The account used to authenticate | `alex.carter` |
| Entitlement | Something the account is permitted to access | Security dashboard |
| Role/group | A collection used to assign entitlements | `GRP-SEC-ANALYSTS` |
| Authorization | The decision that the person should have that access | Approved by role and manager |

```
Alex Carter
Employee LBT-0018
       │
       ├── Department: Technology
       ├── Title: Security Analyst
       └── Manager: Renee Brooks
                  │
                  ▼
          Technical Identity
                  │
                  ▼
          Department Groups
                  │
                  ▼
           Security Role
                  │
                  ▼
             Resources
```

## Identity Authority

The Lazarus company-state system is the authoritative source for
business identity.

Authoritative employee attributes include:

- Employee ID
- Legal/simulated name
- Employment type
- Employment status
- Job title
- Department
- Team
- Manager
- Hire date
- Termination date
- Work location

Technical identity platforms must not become the authoritative source
for employment status or organizational relationships.

```
PostgreSQL / HR
       │
       │ authoritative
       ▼
   IAM Process
       │
       ▼
    Entra ID
```

If PostgreSQL says someone was terminated but Entra still says the
account is enabled, that is a security finding, not merely inconsistent
data.

## Program Authorization

Federal program assignments are independent of organizational
department membership.

Sophia Nguyen as `LBT-0031`, Senior Software Engineer, Engineering does
not by itself authorize ATLAS access. Program access requires an active
approved assignment.

Program assignment records should contain:

- Employee ID
- Program
- Program role
- Assignment start date
- Assignment end date
- Assignment status
- Approval authority

Program access should derive from an active approved assignment rather
than department membership alone.

A later finding of the form “ATLAS assignment expired, ATLAS group still
active” is stale program access.

## Technical Identities

Lazarus may represent identities at multiple levels.

Fifty modeled employees does not require fifty paid cloud users.

### Modeled Identity

Exists in the company-state system but may not have a corresponding
live identity-platform account.

### Active Technical Identity

A modeled employee with a live account in an identity platform.

### Privileged Identity

A separately controlled identity used for administrative activity.

### Service Identity

A non-human identity used by applications, automation, or infrastructure.

Identity type must be distinguishable in inventory and telemetry.

```
IDENTITIES

Human
├── Modeled
├── Active technical
└── Privileged

Non-human
├── Service account
├── Application identity
└── Automation identity
```

## Privileged Identity Separation

Normal employee identities should not receive administrative
permissions solely for convenience.

Where privileged access is required, administrative activity should
be distinguishable from routine user activity.

Privileged access should:

- Have explicit business justification
- Be limited in scope
- Be separately identifiable
- Generate appropriate telemetry
- Be periodically reviewed

The lab operator’s infrastructure-owner access is conceptually separate
from a simulated Security Analyst persona such as Alex Carter. Alex does
not receive god-mode access because the operator needs it.

Exact Entra naming for privileged identities is not decided in this
version.

## Authorization Model

Lazarus will use role- and group-based authorization where practical.

```
               USER
                 │
        ┌────────┼─────────┐
        ▼        ▼         ▼
    Department  Role     Program
      Group     Group      Group
        │        │         │
        └────────┼─────────┘
                 ▼
             RESOURCE
```

Access may derive from:

1. Organizational membership
2. Job function
3. Program assignment
4. Information authorization
5. Administrative responsibility

Direct user-specific permissions should be minimized.

Access must remain traceable to a legitimate business requirement.

Example: Sophia Nguyen may receive `GRP-DEPT-ENGINEERING`,
`GRP-ROLE-SOFTWARE-ENGINEER`, and `GRP-PROGRAM-ATLAS-DEVELOPER`, which
together authorize the ATLAS repository.

Alex Carter may reasonably receive `GRP-DEPT-TECHNOLOGY`,
`GRP-SEC-ANALYSTS`, and `GRP-APP-INTRANET-USERS`. Alex should not
automatically receive `GRP-ADMIN-CLOUD`, `GRP-PROGRAM-ORION-MEMBER`,
`GRP-DATA-RESEARCH-LBT4`, or `GRP-DEPT-HR`.

## Group Taxonomy

Groups use explicit prefixes so access analysis is possible later.

| Pattern | Purpose |
| --- | --- |
| `GRP-DEPT-[DEPARTMENT]` | Organizational membership |
| `GRP-ROLE-[ROLE]` | Job function |
| `GRP-PROGRAM-[PROGRAM]-[ROLE]` | Program assignment |
| `GRP-APP-[APPLICATION]-[ACCESS]` | Application access |
| `GRP-DATA-[DATASET]-[ACCESS]` | Data-domain access |
| `GRP-SEC-[FUNCTION]` | Security function |
| `GRP-ADMIN-[FUNCTION]` | Administrative function |

Examples:

- `GRP-DEPT-ENGINEERING`
- `GRP-PROGRAM-ORION-MEMBER`
- `GRP-PROGRAM-ATLAS-DEVELOPER`
- `GRP-APP-INTRANET-USERS`
- `GRP-DATA-RESEARCH-READ`
- `GRP-SEC-ANALYSTS`
- `GRP-ADMIN-CLOUD`

Names such as `Group7`, `NewSecurityGroup`, `AtlasStuff`, or
`TempUsers2` are not used on Day 0. Naming chaos may be simulated later
as technical debt, not as the initial design.

## Information Authorization

Information classification alone does not grant access.

Lazarus classification labels:

- LBT-1 PUBLIC
- LBT-2 INTERNAL
- LBT-3 CONFIDENTIAL
- LBT-4 CONTROLLED

Authorization to one LBT-4 information domain does not automatically
authorize access to another LBT-4 domain. Proprietary research
authorization does not grant ORION controlled data.

Authorization must consider:

- Classification
- Information domain
- Business role
- Program assignment
- Business need
- Data-owner approval where required

```
Classification
      +
Information domain
      +
Business need
      =
Authorization
```

## Joiner Process

A new employee lifecycle should eventually support:

1. Employee record creation
2. Manager assignment
3. Employment validation
4. Technical identity creation
5. Baseline organizational access
6. Job-function access
7. Approved program access
8. Authentication control enrollment
9. Verification
10. Audit evidence

```
HR creates employee
        │
        ▼
Employment validated
        │
        ▼
Technical identity created
        │
        ▼
Baseline department access
        │
        ▼
Role access
        │
        ▼
Program access if assigned
        │
        ▼
MFA / authentication configured
        │
        ▼
Manager verifies access
        │
        ▼
Employee active
```

## Mover Process

Changes to job function, department, manager, or program assignment
must trigger access reassessment.

The mover process must evaluate both:

- Access that should be granted
- Access that should be removed

Mover events should not simply accumulate additional permissions.

```
OLD ACCESS
    │
    ▼
Determine required change
    │
    ├── Remove obsolete access
    ├── Preserve legitimate access
    └── Add new access
                 │
                 ▼
             Validate
```

## Leaver Process

Termination must trigger timely deprovisioning.

The process should eventually include:

- Disable interactive authentication
- Revoke active sessions where supported
- Remove group and application access
- Address privileged identities
- Address service ownership
- Reassign business resources where necessary
- Preserve required records
- Verify successful deprovisioning

```
Termination event
      │
      ▼
Disable authentication
      │
      ▼
Revoke active sessions
      │
      ▼
Remove access
      │
      ▼
Handle privileged identities
      │
      ▼
Handle owned resources
      │
      ▼
Preserve required records
      │
      ▼
Verify deprovisioning
```

Leaver failures may be introduced later by simulation. They are not
planted in Day 0.

## Access Requests

Non-baseline access should require documented business justification.

Approval requirements may depend on:

- Resource sensitivity
- Program
- Information classification
- Privilege level

Sensitive access should be approved by an appropriate business or data
owner rather than solely by technical administrators.

A Security Analyst requesting HORIZON is not automatically justified by
job title. Expected path: request → manager approval → program/data
owner approval → IAM provisioning → evidence recorded.

## Access Reviews

Lazarus must eventually support periodic review of sensitive access.

Reviews should identify:

- User
- Resource
- Entitlement
- Business justification
- Approver
- Review decision
- Review date

Possible decisions include:

- Retain
- Remove
- Modify
- Investigate

Review evidence should be preserved for governance analysis.

## Identity Telemetry

Identity-related events should be observable where supported.

Relevant events include:

- Successful authentication
- Failed authentication
- MFA activity
- Account creation
- Account disablement
- Group membership changes
- Privileged role changes
- Access assignment changes
- Application authentication

Identity telemetry should eventually be correlated with the company-state
employee record.

```
Identity event
      ↓
Entra / application
      ↓
Log source
      ↓
Wazuh / later Sentinel
      ↓
Analyst
```

A useful alert includes more than a username: employee ID, department,
role, account status, and source context from company state.

## Day-0 Security Posture

Initial identity configuration should represent a reasonably designed
least-privilege environment.

Known security failures should not be intentionally introduced during
initial deployment merely to create findings.

Future simulation phases may introduce lifecycle failures,
misconfiguration, excessive access, stale entitlements, or other
identity-control failures.

Where possible, analyst-facing scenarios should not reveal the expected
finding before investigation. The simulation engine may hold ground
truth; the analyst sees evidence.

## Day-0 Access Catalog

The initial structured access catalog is
[day0-access-model.csv](../../data/governance/day0-access-model.csv).

## Related Documents

- [Enterprise requirements](enterprise-requirements.md)
- [Logical architecture](logical-architecture.md)
- [Network architecture](network-architecture.md)
- [Identity architecture diagram v0.1](diagrams/identity-architecture-v0.1.md)
- [ADR-002 Identity authority](../decisions/ADR-002-identity-authority.md)
- [Information classification](../02-information-governance/information-classification.md)
- [Workforce roster](../01-company/workforce-roster.md)
