# Logical Architecture Diagram — v0.1

**Document:** LBT-ARCH-001  
**Version:** 0.1  
**Status:** Draft  
**Date:** 2026-09-21

This is the first logical blueprint of Lazarus Biotechnologies. It is
intentionally ASCII. Polished portfolio diagrams come later.

Lazarus is fictional. This diagram describes a simulated enterprise, not
an employer or production environment.

```
                         LAZARUS BIOTECHNOLOGIES
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│                       BUSINESS LAYER                                │
│                                                                     │
│   Employees ─ Departments ─ Managers ─ Programs ─ Data Owners       │
│       │                                                             │
└───────┼─────────────────────────────────────────────────────────────┘
        │
        ▼
┌──────────────────────────────┐
│       COMPANY STATE          │
│                              │
│        PostgreSQL            │
│                              │
│ Employees                    │
│ Departments                  │
│ Program assignments          │
│ Information authorization    │
│ Asset relationships          │
└──────────────┬───────────────┘
               │
       ┌───────┴───────────┐
       ▼                   ▼
┌──────────────┐     ┌───────────────────┐
│   IDENTITY   │     │ SIMULATION ENGINE │
│              │     │                   │
│ Entra ID     │     │ Python            │
│ Accounts     │     │ Schedules         │
│ Groups       │     │ Personas          │
│ Roles        │     │ Business activity │
│ MFA          │     │ Lifecycle events  │
└──────┬───────┘     └─────────┬─────────┘
       │                       │
       └────────────┬──────────┘
                    ▼
          ┌───────────────────┐
          │ BUSINESS SERVICES │
          │                   │
          │ Internal portal   │
          │ Data resources    │
          │ Engineering       │
          │ Program resources │
          └─────────┬─────────┘
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
    ┌───────────┐       ┌───────────┐
    │ WINDOWS   │       │   LINUX   │
    │ ENDPOINTS │       │  SYSTEMS  │
    └─────┬─────┘       └─────┬─────┘
          │                   │
          └─────────┬─────────┘
                    │
                    ▼
        ┌─────────────────────────┐
        │   SECURITY TELEMETRY    │
        │                         │
        │ Authentication          │
        │ Endpoint                │
        │ Application             │
        │ System                  │
        │ Network                 │
        └────────────┬────────────┘
                     │
                     ▼
             ┌──────────────┐
             │    WAZUH     │
             │              │
             │ Collection   │
             │ Detection    │
             │ Search       │
             │ Dashboards   │
             └──────┬───────┘
                    │
                    ▼
            ┌───────────────┐
            │ SECURITY      │
            │ ANALYST       │
            │ Alex Carter   │
            └───────┬───────┘
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
    Investigation         Remediation
          │                   │
          └─────────┬─────────┘
                    ▼
             COMPANY STATE
                CHANGES
```

The final loop is required: investigation and remediation must be able
to change persistent company state. The environment does not reset after
every exercise.
