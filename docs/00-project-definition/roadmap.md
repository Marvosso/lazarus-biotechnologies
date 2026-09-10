# Lazarus Biotechnologies Master Roadmap

**Project:** Lazarus Biotechnologies Virtual Enterprise  
**Status:** Active  
**Current Phase:** Phase 0 — Foundation

---

# Phase 0 — Foundation

## 00.01 Project Charter
Define the purpose, goals, constraints, and intended outcomes.

## 00.02 Company Creation
Create the fictional business, organizational structure, business lines,
workforce, and initial operating model.

## 00.03 Information Governance
Define information classifications, data ownership, and crown jewels.

## 00.04 Scope & Constraints
Define budget, local/cloud boundaries, simulation boundaries, and
security/safety constraints.

## 00.05 V0.1 Success Criteria
Define the minimum conditions required for the virtual company to be
considered operational.

## 00.06 Repository Initialization
Create the Git repository, public GitHub repository, initial structure,
and project history.

## 00.07 Documentation Standard
Establish implementation, troubleshooting, evidence, ADR, and versioning
standards.

## 00.08 Master Roadmap
Define the implementation sequence for the full environment.

## 00.09 Portfolio Architecture
Design how project evidence, milestones, skills, screenshots, case
studies, and historical snapshots will be published.

---

# Phase 1 — Enterprise Architecture

## 01.01 Requirements Mapping
Map business requirements to technology requirements.

## 01.02 Logical Architecture
Design identity, endpoints, applications, infrastructure, networking,
logging, and security components.

## 01.03 Network Architecture
Define lab networks, segmentation, addressing, and isolation.

## 01.04 Identity Architecture
Design HR-to-identity relationships, accounts, groups, roles, and
privileged access.

## 01.05 Data Flow Architecture
Document how information moves between users, systems, and services.

## 01.06 Security Architecture
Define initial defensive controls and telemetry sources.

## 01.07 Architecture Baseline
Publish the first approved enterprise architecture version.

---

# Phase 2 — Core Infrastructure

## 02.01 Host Assessment
Determine available CPU, RAM, storage, virtualization features, and
network capabilities.

## 02.02 Virtualization Platform
Configure the local virtualization environment.

## 02.03 Lab Networking
Create isolated virtual networks and routing boundaries.

## 02.04 Linux Foundation
Deploy initial Linux infrastructure.

## 02.05 Windows Foundation
Deploy representative Windows systems.

## 02.06 Core Services
Establish DNS, time synchronization, administration, and supporting
services where required.

## 02.07 Infrastructure Validation
Verify connectivity, isolation, resource utilization, and recoverability.

---

# Phase 3 — Company State & Business Systems

## 03.01 PostgreSQL
Deploy the Lazarus company-state database.

## 03.02 HR Data Model
Import the authoritative workforce roster.

## 03.03 Organization Model
Represent departments, managers, employment status, and business units.

## 03.04 Program Assignments
Model ORION, ATLAS, HORIZON, and future program assignments separately
from organizational roles.

## 03.05 Information Authorization
Model data authorization and need-to-know relationships.

## 03.06 Business Applications
Deploy lightweight internal applications required for normal simulated
operations.

## 03.07 Asset Registry
Create the initial enterprise asset inventory.

---

# Phase 4 — Identity & Access Management

## 04.01 Identity Source of Truth
Define HR as the authoritative business identity source.

## 04.02 Microsoft Entra Foundation
Create the cloud identity environment where feasible.

## 04.03 Initial Active Users
Provision a representative subset of Lazarus employees as real identities.

## 04.04 Groups & Roles
Implement department, program, application, and administrative groups.

## 04.05 Authentication Controls
Configure secure authentication and MFA where available.

## 04.06 Joiner Workflow
Design and test user onboarding.

## 04.07 Mover Workflow
Design and test department/program changes.

## 04.08 Leaver Workflow
Design and test employee termination/offboarding.

## 04.09 Access Reviews
Establish initial access-review procedures and evidence.

## 04.10 IAM Baseline
Record identity-security metrics and known gaps.

---

# Phase 5 — Endpoint & User Environment

## 05.01 Endpoint Personas
Determine which employee roles require representative real endpoints.

## 05.02 Windows Endpoint
Configure the primary Windows user endpoint.

## 05.03 Linux Endpoint
Configure a representative technical Linux endpoint.

## 05.04 Administrative Endpoint
Create a controlled administrative workstation if needed.

## 05.05 Endpoint Logging
Enable appropriate host telemetry.

## 05.06 Security Baseline
Apply initial secure configurations.

## 05.07 Endpoint Inventory
Link endpoints to modeled users and asset records.

---

# Phase 6 — Centralized Logging & SIEM

## 06.01 Logging Requirements
Define which events must be observable.

## 06.02 Wazuh Deployment
Deploy the local security monitoring platform.

## 06.03 Windows Telemetry
Forward Windows security events.

## 06.04 Linux Telemetry
Forward Linux system/authentication events.

## 06.05 Application Telemetry
Ingest logs from Lazarus applications.

## 06.06 Identity Telemetry
Integrate available authentication and identity events.

## 06.07 Asset Context
Associate security events with users, assets, departments, and programs.

## 06.08 Initial Dashboards
Build operational security views.

## 06.09 Logging Coverage Assessment
Measure which systems are visible and which are not.

---

# Phase 7 — Normal Business Simulation

## 07.01 Simulation Engine Design
Define architecture for the company activity simulator.

## 07.02 Employee Personas
Create behavior profiles based on job roles.

## 07.03 Work Schedules
Model working hours, remote/hybrid behavior, and activity frequency.

## 07.04 Authentication Activity
Generate legitimate authentication behavior.

## 07.05 Business Application Activity
Generate routine application usage.

## 07.06 Data Access Activity
Generate legitimate file/data interaction.

## 07.07 Engineering Activity
Simulate development and technical workflows.

## 07.08 Federal Program Activity
Generate program-specific business behavior.

## 07.09 Normal Activity Baseline
Establish what normal Lazarus behavior looks like.

---

# Phase 8 — V0.1 Validation: The Company Is Alive

## 08.01 End-to-End Activity Test
Confirm simulated business activity creates observable real telemetry.

## 08.02 Random Employee Investigation
Select a modeled employee and reconstruct activity using security
telemetry rather than simulator ground truth.

## 08.03 Visibility Gap Assessment
Identify missing telemetry or context.

## 08.04 Remediation
Correct significant visibility gaps.

## 08.05 V0.1 Acceptance
Declare the first living-company milestone complete.

## 08.06 Portfolio Snapshot
Publish the V0.1 architecture, findings, evidence, and lessons learned.

---

# Phase 9 — Vulnerability Management

## 09.01 Vulnerability Management Standard
Define severity, ownership, SLAs, and remediation workflow.

## 09.02 Greenbone/OpenVAS
Deploy a free vulnerability scanning capability.

## 09.03 Initial Assessment
Scan authorized Lazarus systems.

## 09.04 Validation
Distinguish true findings from false positives.

## 09.05 Asset & Business Context
Connect technical vulnerabilities to affected systems and crown jewels.

## 09.06 Remediation
Resolve selected vulnerabilities.

## 09.07 Retesting
Verify remediation.

## 09.08 Vulnerability Metrics
Create backlog, aging, SLA, and risk metrics.

---

# Phase 10 — Human Error & Control Failures

## 10.01 Scenario Framework
Create controlled non-malicious security scenarios.

## 10.02 Excessive Access
Introduce access inconsistent with business need.

## 10.03 Stale Access
Allow access to remain after a program or job change.

## 10.04 Data Misplacement
Place sensitive synthetic data in an inappropriate location.

## 10.05 Configuration Drift
Introduce controlled configuration deviations.

## 10.06 Logging Failure
Create temporary telemetry gaps.

## 10.07 Analyst Investigation
Investigate without viewing scenario ground truth.

## 10.08 Control Improvements
Implement preventive and detective controls.

---

# Phase 11 — Detection Engineering

## 11.01 Detection Standard
Define how detections are written, tested, documented, and maintained.

## 11.02 Authentication Detections
Build identity-focused detections.

## 11.03 Privilege Detections
Detect suspicious privileged activity.

## 11.04 Endpoint Detections
Create endpoint-focused rules.

## 11.05 Data Access Detections
Identify abnormal access to sensitive resources.

## 11.06 Detection Testing
Generate controlled activity to verify detection logic.

## 11.07 Tuning
Reduce unnecessary noise and false positives.

## 11.08 Detection Metrics
Measure effectiveness and coverage.

---

# Phase 12 — Incident Response

## 12.01 Incident Response Plan
Create the Lazarus IR lifecycle.

## 12.02 Case Management
Create incident numbering and documentation processes.

## 12.03 Initial Alert Handling
Practice triage.

## 12.04 Investigation
Perform timeline, scope, user, and asset analysis.

## 12.05 Containment
Implement controlled containment actions.

## 12.06 Recovery
Return systems to normal operations.

## 12.07 Lessons Learned
Record control failures and corrective actions.

---

# Phase 13 — Controlled Attack Simulation

## 13.01 Cyber Range
Build the isolated attack-testing environment.

## 13.02 Adversary Simulation Rules
Define authorized techniques and safety controls.

## 13.03 Credential Abuse Scenarios
Test controlled identity compromise.

## 13.04 Endpoint Attack Scenarios
Generate authorized endpoint activity.

## 13.05 Lateral Movement Scenarios
Practice detection in the isolated environment.

## 13.06 Detection & Investigation
Respond using analyst-visible evidence only.

## 13.07 Ground Truth Review
Compare investigation conclusions against the scenario engine after case
closure.

---

# Phase 14 — GRC & Security Governance

## 14.01 Control Framework Mapping
Map selected controls to relevant standards.

## 14.02 NIST SP 800-171 Learning Track
Study and map applicable concepts for the simulated federal environment.

## 14.03 Security Policies
Create realistic organizational policies.

## 14.04 Risk Register
Establish a formal risk-management process.

## 14.05 POA&M-Style Remediation
Track unresolved control weaknesses.

## 14.06 Security Evidence
Collect evidence for implemented controls.

## 14.07 Access Governance
Formalize recurring access reviews and approvals.

## 14.08 Security Maturity Assessment
Measure posture against the initial baseline.

---

# Phase 15 — Security Analytics & Power BI

## 15.01 Security Data Model
Combine HR, IAM, asset, vulnerability, incident, and risk data.

## 15.02 Identity Dashboard
Build IAM/security-governance analytics.

## 15.03 Vulnerability Dashboard
Build remediation and risk views.

## 15.04 SOC Dashboard
Build alert, incident, and response metrics.

## 15.05 Risk Dashboard
Visualize crown-jewel and control risk.

## 15.06 Executive Dashboard
Translate technical findings into business-level reporting.

---

# Phase 16 — Cloud Security Expansion

## 16.01 Azure Security Baseline
Implement selected Azure resources within cost constraints.

## 16.02 Entra Security Expansion
Introduce additional identity controls.

## 16.03 Microsoft Sentinel Exercise
Send a controlled volume of Lazarus telemetry to Sentinel.

## 16.04 KQL Detection Engineering
Build and test Sentinel queries and detections.

## 16.05 Cloud Cost Review
Document actual cloud cost and optimization decisions.

---

# Phase 17 — Automated Company Evolution

## 17.01 Lifecycle Engine
Automate hires, transfers, promotions, and terminations.

## 17.02 Technology Change
Introduce applications, systems, and software versions over time.

## 17.03 Security Drift
Allow realistic control degradation and configuration drift.

## 17.04 Business Growth
Expand departments, programs, and employee population.

## 17.05 Historical State
Preserve snapshots of company and security posture.

---

# Phase 18 — AI Employee Behavior

## 18.01 AI Design
Define where AI agents add value beyond deterministic simulation.

## 18.02 Employee Agents
Create selected employee personas.

## 18.03 Behavioral Variation
Introduce more realistic business interactions.

## 18.04 Security Boundaries
Ensure agents cannot interact with unauthorized external systems.

## 18.05 AI Security Testing
Assess prompt, identity, and authorization risks introduced by AI agents.

---

# Phase 19 — Platform Integration

## 19.01 SentinelView Integration
Connect enterprise risk information to SentinelView.

## 19.02 AccessFlow Integration
Connect IAM lifecycle and access-governance information.

## 19.03 Additional Projects
Use Lazarus as a source of realistic data for future portfolio work.

---

# Phase 20 — Mature Living Enterprise

The project transitions from a build project into an evolving virtual
organization.

Normal operations continue.

Employees join and leave.

Systems change.

Vulnerabilities appear.

Security incidents occur.

Controls improve.

Security posture is measured over time.

The environment remains a persistent cybersecurity learning platform.
