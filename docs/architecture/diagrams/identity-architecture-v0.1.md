# Identity Architecture Diagram — v0.1

**Document:** LBT-ARCH-IAM-001  
**Version:** 0.1  
**Status:** Draft  
**Date:** 2026-09-21

This is the first identity relationship blueprint of Lazarus
Biotechnologies. It is intentionally ASCII. Polished portfolio diagrams
come later.

Lazarus is fictional. This diagram describes a simulated enterprise, not
an employer or production environment.

```
                         HR / COMPANY STATE
                                │
                                ▼
                            EMPLOYEE
                                │
                ┌───────────────┼───────────────┐
                ▼               ▼               ▼
           DEPARTMENT       JOB ROLE        MANAGER
                                │
                                ▼
                      PROGRAM ASSIGNMENTS
                                │
                                ▼
                     INFORMATION AUTHORIZATION
                                │
                                ▼
                       TECHNICAL IDENTITY
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                 ▼
        DEPARTMENT GROUP     ROLE GROUP       PROGRAM GROUP
              │                 │                 │
              └─────────────────┼─────────────────┘
                                ▼
                           ENTITLEMENTS
                                │
                                ▼
                             RESOURCE
                                │
                                ▼
                            TELEMETRY
                                │
                                ▼
                         SECURITY ANALYST
```

Company state is authoritative for who the employee is. Entra (or another
identity platform) is authoritative for authentication of active
technical identities. Program assignments are independent of department.
Day 0 does not include planted stale access.
