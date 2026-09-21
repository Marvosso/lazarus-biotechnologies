# Data Flow Diagram — v0.1

**Document:** LBT-ARCH-DATA-001  
**Version:** 0.1  
**Status:** Draft  
**Date:** 2026-09-21

This is the first data-flow blueprint of Lazarus Biotechnologies. It is
intentionally ASCII. Polished portfolio diagrams come later.

Lazarus is fictional. This diagram describes a simulated enterprise, not
an employer or production environment. Synthetic controlled artifacts
must be labeled: SIMULATED TRAINING DATA — NOT ACTUAL CUI.

```
                    ┌─────────────────┐
                    │ HR / COMPANY    │
                    │ STATE           │
                    └───────┬─────────┘
                            │
                            ▼
                    ┌─────────────────┐
                    │ IDENTITY        │
                    └───────┬─────────┘
                            │
                            ▼
EMPLOYEE ──────► ENDPOINT ──────► BUSINESS APPLICATION
                    │                     │
                    │                     ▼
                    │                DATA STORE
                    │                     │
                    │                     │
                    ▼                     ▼
               TELEMETRY ◄────────────────┘
                    │
                    ▼
                  SIEM
                    │
                    ▼
             SECURITY ANALYST
                    │
                    ▼
               INVESTIGATION
                    │
                    ▼
                REMEDIATION
                    │
       ┌────────────┼─────────────┐
       ▼            ▼             ▼
    IDENTITY      SYSTEM       GOVERNANCE
     CHANGE       CHANGE         CHANGE
```

High-value example (DF-004): Emily Davis (LBT-0046) uses a User Zone
endpoint (`10.10.10.x`) over HTTPS to an ORION service (`10.10.20.x`).
The application, not the workstation, reaches the datastore. Access
requires an active ORION assignment. When that assignment expires,
ORION entitlement is removed; the employee identity remains active.
