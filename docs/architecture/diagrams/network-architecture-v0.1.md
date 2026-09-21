# Network Architecture Diagram — v0.1

**Document:** LBT-ARCH-NET-001  
**Version:** 0.1  
**Status:** Draft  
**Date:** 2026-09-21

This is the first logical network blueprint of Lazarus Biotechnologies.
It is intentionally ASCII. Polished portfolio diagrams come later.

Lazarus is fictional. This diagram describes a simulated enterprise, not
an employer or production environment.

No hosts in this diagram are deployed yet. Addresses are reserved.

```
                         INTERNET
                            │
                  ┌─────────┴─────────┐
                  │                   │
                  ▼                   ▼
          Microsoft Cloud         LAB EDGE
          Entra / Azure               │
                                      │
            ┌─────────────────────────┼─────────────────────────┐
            │                         │                         │
            ▼                         ▼                         ▼
      USER ZONE                 SERVER ZONE              MANAGEMENT
    10.10.10.0/24             10.10.20.0/24            10.10.30.0/24
            │                         │                         │
            │                         │                         │
            └─────────────┬───────────┘                         │
                          │                                     │
                          ▼                                     │
                   SECURITY ZONE ◄──────────────────────────────┘
                   10.10.40.0/24
                          │
                     restricted
                          │
                          ▼
                    CYBER RANGE
                   10.10.50.0/24


                  FUTURE DMZ
                 10.10.60.0/24
```

Expected later application path (not a firewall policy yet):

```
LBT-WIN-01  10.10.10.100
     │ HTTPS
     ▼
LBT-APP-01  10.10.20.20
     │ PostgreSQL
     ▼
LBT-DB-01   10.10.20.10

Telemetry from WIN / APP / DB → LBT-SIEM-01 10.10.40.10

Direct WIN-01 → DB-01:5432 should generally not be necessary.
```
