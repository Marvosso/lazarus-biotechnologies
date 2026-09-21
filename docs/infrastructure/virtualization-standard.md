# Lazarus Virtualization Standard

**Document ID:** LBT-INF-VIRT-001  
**Platform:** Microsoft Hyper-V  
**Version:** 0.1  
**Status:** Accepted — Hyper-V enabled, verified after reboot, no Lazarus VMs deployed  
**Date:** 2026-09-21

> **Disclaimer:** Lazarus Biotechnologies is entirely fictional. This standard applies to a simulated enterprise lab. No actual classified information, CUI, patient information, government data, or customer data is used.

Related decision: [ADR-004](../decisions/ADR-004-hyper-v-platform.md).  
Host assessment: [host-assessment.md](host-assessment.md).

## VM Naming

Virtual machines use:

`LBT-[FUNCTION]-[NUMBER]`

Examples:

- LBT-WIN-01
- LBT-INFRA-01
- LBT-SIEM-01
- LBT-SEC-01
- LBT-RANGE-01

## VM Generation

Generation 2 is the default.

Generation 1 will only be used where a documented compatibility
requirement exists.

## CPU

vCPU allocations should begin conservatively and increase only when
observed workload requirements justify additional resources.

## Memory

Memory allocation must account for the host's approximately 32 GB
physical-memory limit.

Normal Lazarus operation should target approximately 8–10 GB total RAM.

Temporary expanded operation may use approximately 12–14 GB when host
workload permits.

Dynamic Memory may be used where appropriate for compatible
general-purpose guests.

Security platforms, databases, and other memory-sensitive workloads will
be evaluated individually rather than automatically configured with
Dynamic Memory.

Actual memory utilization will be measured after deployment.

## Storage

Virtual disks should initially use dynamically expanding VHDX files
unless a workload demonstrates a requirement for another configuration.

## Host Storage Standard

Lazarus virtualization assets should be stored under a dedicated host
directory rather than mixed with project source code.

Proposed root:

`C:\LazarusLab\`

Eventual layout:

```
C:\LazarusLab\
│
├── VMs\
├── VirtualDisks\
├── ISOs\
├── Backups\
└── Exports\
```

Virtual-machine disks and ISO images must not be committed to Git.

```
GitHub repository
        │
        ├── architecture
        ├── configs
        ├── scripts
        ├── evidence
        └── documentation

C:\LazarusLab
        │
        ├── VHDX
        ├── ISO
        ├── VM state
        └── backups
```

The repo describes/reproduces the environment. The repo is not the
environment.

## Checkpoints

Checkpoints may be used before significant lab changes or experiments.

Checkpoints are not backups.

Long-lived unnecessary checkpoints should be removed after validation.

## Networking

VM network connectivity must follow the approved Lazarus network
architecture.

Convenience networking must not replace documented security-zone
placement.

Do not use Default Switch as the Lazarus enterprise topology.

Hyper-V switch types for later lab networking:

| Type | Host participates | Typical use |
| --- | --- | --- |
| External | Via physical adapter | Controlled internet/LAN access |
| Internal | Yes | Host-to-VM and VM-to-VM |
| Private | No | Isolated VM-to-VM (including cyber range) |

Lazarus zones (`10.10.10.0/24` through `10.10.60.0/24`) will be created
in 02.03. They are not created in this step.

## Security

Cyber-range systems must remain isolated according to the approved
network architecture.

Credentials, private keys, and sensitive configuration must not be
committed to the public repository.

## Implementation Record

### Initial State

- Windows 11 Pro
- Hardware virtualization enabled
- VBS active
- No VMware installation detected
- No VirtualBox installation detected
- No Lazarus virtual machines deployed

### Pre-Implementation State

Hyper-V full feature state:

Not verified via `Get-WindowsOptionalFeature` (requires Administrator).
Management components are absent, which is consistent with **Disabled**:

- `vmms` service: not present
- `Get-VM`: cmdlet not recognized
- Hyper-V Manager (`virtmgmt.msc`): not present
- Hyper-V PowerShell module: not listed

Hardware virtualization:

Enabled

Existing hypervisor/VBS:

Active. `HvHost` (HV Host Service) is **Running**. Guest integration
services exist but are stopped on the host (expected). This matches the
earlier host assessment: a hypervisor is detected for VBS, not a ready
Hyper-V VM platform.

No Lazarus virtual switches or VMs exist.

### Decision

Microsoft Hyper-V selected as the V0.1 virtualization platform.

### Changes Performed

Operator enabled `Microsoft-Hyper-V-All` from an elevated PowerShell
session. Evidence: `Get-WindowsOptionalFeature` reported
`State : Enabled` with `RestartRequired : Possible`.

This Cursor session did not run the enable command.

### Verification

Pre-reboot (2026-09-21 ~17:08): feature Enabled, management stack absent.
See Issues Encountered.

Post-reboot Administrator verification (2026-09-21):

| Check | Result |
| --- | --- |
| LastBootUpTime | 2026-09-21 17:13:53 |
| CBS RebootPending | False |
| Hyper-V feature `Microsoft-Hyper-V-All` | Enabled |
| `vmms` service | Running (Automatic) — Hyper-V Virtual Machine Management |
| `Get-VM` cmdlet | Present (Hyper-V module 2.0.0.0) |
| VM enumeration | Empty — 0 virtual machines |
| Virtual-switch enumeration | `Default Switch` (`Internal`) only |

Default Switch is Hyper-V convenience networking. It must not define Lazarus
security zones. Lazarus networks will be created in 02.03.

### Issues Encountered

A hypervisor for VBS was already running. Enabling `Microsoft-Hyper-V-All`
marked the feature Enabled, but Hyper-V Manager, `vmms`, and the Hyper-V
PowerShell module are not available until the host restarts.

Post-enable verification (Administrator PowerShell, 2026-09-21):

```
Get-Service vmms          → service not found
Get-Command Get-VM        → cmdlet not recognized
Get-VM                    → cmdlet not recognized
Get-VMSwitch              → cmdlet not recognized
```

Windows reports Hyper-V optional features as Enabled (`Win32_OptionalFeature`
InstallState = 1 for `Microsoft-Hyper-V-All` and management subfeatures),
but `vmms.exe` and `virtmgmt.msc` are still not on disk.

`Component Based Servicing\RebootPending` remains present.

Host `LastBootUpTime` at 2026-09-21 17:08 was still **2026-09-19 16:38**.
The current Windows session has not completed the post-enable reboot,
so the management stack never installed.

A Start-menu restart that is skipped by Fast Startup, or restarting only
a terminal/app, is not sufficient. A full OS restart is required:

```
shutdown /r /t 0
```

Do not enable additional features until after that reboot.

A full restart at 17:13:53 installed the management stack. Administrator
verification confirmed `vmms` Running, `Get-VM` available, zero VMs, and
only the Default Switch. No Lazarus VMs or zone switches were created.

## 02.02 Validation Checklist

- [x] Hyper-V feature enabled
- [x] Hyper-V management available (`vmms` Running; `virtmgmt.msc` present)
- [x] Get-VM works
- [x] Existing virtual switches enumerated (`Default Switch`, Internal)
- [x] No Lazarus VMs created prematurely
- [x] Virtualization standard documented
- [x] Architecture decision documented
- [x] Host remains stable after reboot
