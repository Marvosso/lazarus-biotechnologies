# Lazarus Biotechnologies Host Assessment

**Document ID:** LBT-INF-HOST-001  
**Status:** Complete  
**Phase:** 2 — Core Infrastructure  
**Assessment Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This assessment describes personal lab hardware used to host a simulated enterprise. No actual classified information, CUI, patient information, government data, or customer data is used.

## Purpose

This assessment evaluates the physical Lazarus lab host to determine
realistic virtualization, containerization, storage, and networking
capacity.

The results will determine the initial infrastructure deployment model.

Nothing was installed or enabled during this assessment. Hyper-V, WSL,
and Docker were not turned on.

Collected values omit serial numbers, product keys, MAC addresses,
public IPs, usernames, and device identifiers.

## Host Specifications

| Attribute | Value |
| --- | --- |
| CPU | Intel Core i7-11800H |
| Physical Cores | 8 |
| Logical Processors | 16 |
| Installed RAM | 31.75 GB |
| Normal Light-Session RAM Use | ~13.3 GB |
| Heavy-Session RAM Use | ~18.8 GB |
| Heavy-Session Available RAM | ~12.9 GB |
| GPU | NVIDIA RTX 3080 Laptop + Intel UHD |
| Windows Edition | Windows 11 Pro |
| Windows Build | 26200 |
| Virtualization Enabled | Yes |
| Existing Hypervisor State | Hypervisor detected / VBS active |
| WSL | Not installed |
| Docker | Not installed |
| VMware / VirtualBox | Not found |
| Primary Storage | NVMe SSD |
| Storage Capacity | ~954 GB |
| Available Storage | ~486 GB |

## Collection Notes

- `Get-ComputerInfo` reported `Windows 10 Pro`; `systeminfo` reported `Microsoft Windows 11 Pro`. Build `10.0.26200` is Windows 11. The edition used here is Windows 11 Pro.
- `Get-WindowsOptionalFeature -Online` requires elevation and was not run. Optional-feature state is deferred to 02.02.
- `systeminfo` Hyper-V requirements: "A hypervisor has been detected. Features required for Hyper-V will not be displayed."
- WSL: not installed (`wsl.exe --install` was not run).
- Docker CLI: not present.
- `Get-Package` found no VMware, VirtualBox, or Docker products.
- Heavy-session RAM (18.8 GB / 31.7 GB, 59% in use, ~12.9 GB available) was reported by the operator from Task Manager during a representative gaming/desktop session.

## Capacity Assessment

### CPU Capacity — GOOD

The Intel Core i7-11800H provides 8 physical cores and 16 logical
processors.

This is sufficient for the initial Lazarus environment. Virtual CPU
resources may be moderately oversubscribed because most lab workloads
will not simultaneously sustain maximum CPU utilization.

CPU-intensive activities such as vulnerability scanning should be
scheduled rather than assumed to run continuously.

### Memory Capacity — CONSTRAINED BUT SUFFICIENT

The host contains approximately 32 GB of RAM.

Observed memory usage:

- Light/current session: approximately 13.3 GB
- Representative heavy session: approximately 18.8 GB
- Remaining physical memory during heavy use: approximately 12.9 GB

Memory is therefore the primary infrastructure constraint.

Lazarus should not reserve 16 GB or more of memory permanently.

Initial design target:

- Normal Lazarus operation: approximately 8–10 GB
- Temporary expanded lab operation: approximately 12–14 GB
- High-memory security workloads should be started only when required.
- Cyber-range and vulnerability-scanning workloads do not need to run
  continuously.
- Unnecessary VMs should remain powered off.

### Storage Capacity — GOOD

Approximately 486 GB of NVMe storage is currently available.

An initial Lazarus storage budget of approximately 200–250 GB is
reasonable while retaining significant host free-space headroom.

Storage consumption should be monitored as VM snapshots, security
telemetry, vulnerability data, and backups accumulate.

### Virtualization Capability — GOOD

Hardware virtualization is enabled.

Windows reports an active hypervisor environment and VBS is currently
running.

The host is therefore suitable for virtualization, subject to final
hypervisor selection during Step 02.02.

### Overall Lab Capacity — SUFFICIENT FOR V0.1

The host is suitable for Lazarus Biotechnologies V0.1.

CPU and storage capacity are strong.

Memory is the primary limiting resource and requires a resource-efficient
architecture using a combination of virtual machines and containers.

The environment should favor representative systems rather than
one-system-per-business-function deployment.

## Resource Envelope

| Resource | Normal target | Temporary ceiling |
| --- | ---: | ---: |
| Lazarus RAM | **8–10 GB** | **12–14 GB** |
| Lazarus active vCPU | ~6–10 vCPU allocated across VMs | ~12–16 vCPU allocated |
| Lazarus storage | ~200 GB initially | ~250 GB before review |
| Persistent VMs | 2–3 | — |
| Concurrent heavy workloads | 1 | — |

vCPU numbers are virtual allocations and may be oversubscribed
moderately. RAM numbers are the binding constraint.

## Resource-Efficient Deployment Direction

Four permanently running chunky VMs is not the target.

```
WINDOWS 11 HOST
31.75 GB RAM
│
├── LBT-INFRA-01
│   Linux
│   ~2 GB
│   │
│   └── Containers
│       ├── PostgreSQL
│       ├── Lazarus internal application
│       └── Simulation engine
│
├── LBT-WIN-01
│   Windows endpoint
│   ~4 GB
│
├── LBT-SIEM-01
│   Wazuh
│   ~4–6 GB
│   └── Run when required / tune carefully
│
└── ON-DEMAND SYSTEMS
    │
    ├── Vulnerability scanner
    └── Cyber range
```

These RAM figures will be adjusted after observed consumption.
Dynamic memory for some guests may be considered after hypervisor
selection in 02.02.

## Assessment Finding — HOST-001

### Finding

Memory is the primary physical constraint for the Lazarus environment.

### Evidence

The 31.75 GB host consumed approximately 18.8 GB during a representative
heavy desktop/gaming session.

### Impact

Running multiple high-memory virtual machines continuously could cause
host memory pressure and degrade normal host performance.

### Decision

Lazarus will use a resource-efficient deployment model combining
virtualization, containerization, and on-demand security workloads.

Normal lab consumption should target approximately 8–10 GB RAM.

### Architecture Impact

Architecture v0.1 remains viable.

No architecture revision is currently required because the original
design explicitly allowed representative systems and simulated scale.

Exact VM allocation will be determined during virtualization and core
infrastructure implementation.
