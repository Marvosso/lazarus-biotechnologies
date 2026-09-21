# Security Architecture Diagram — v0.1

**Document:** LBT-ARCH-SEC-001  
**Version:** 0.1  
**Status:** Draft  
**Date:** 2026-09-21

This is the first security-architecture blueprint of Lazarus
Biotechnologies. It is intentionally ASCII. Polished portfolio diagrams
come later.

Lazarus is fictional. This diagram describes a simulated enterprise, not
an employer or production environment.

```
                           INTERNET
                              │
                      EXTERNAL BOUNDARY
                              │
               ┌──────────────┴──────────────┐
               ▼                             ▼
          CLOUD IDENTITY                 LAB EDGE
               │                             │
               │                 ┌───────────┼───────────┐
               │                 ▼           ▼           ▼
               │              USERS       SERVERS    MANAGEMENT
               │                 │           │           │
               └─────────────────┼───────────┼───────────┘
                                 │           │
                                 ▼           ▼
                              IDENTITY      DATA
                                 │           │
                                 └─────┬─────┘
                                       │
                         ┌─────────────▼─────────────┐
                         │      CROWN JEWELS         │
                         └───────────────────────────┘

                     SECURITY VISIBILITY
        Identity ──────────────┐
        Endpoint ──────────────┤
        Application ───────────┤
        Server ────────────────┼────► WAZUH ───► ANALYST
        Network ───────────────┤
        Vulnerability ─────────┘

                         ISOLATED BOUNDARY
                                │
                                ▼
                           CYBER RANGE
```

Wazuh is the planned persistent local SIEM. Sentinel is a later
controlled cloud exercise, not the V0.1 system of record.
