# Homelab Detection and Response Portfolio

> Hands-on blue team homelab built from bare metal. Each lab documents the full process — infrastructure, deployment, troubleshooting, and detection engineering.

**GitHub:** [Jery481-rev](https://github.com/Jery481-rev) | **Repo:** [Homlab-Detection-response-portfolio](https://github.com/Jery481-rev/Homlab-Detection-response-portfolio)

---

## Lab Index

| Lab | Focus | Status |
|-----|-------|--------|
| [Day 01 — Wazuh SIEM + Windows Endpoint](#day-01-proxmox-wazuh-siem-and-windows-endpoint-setup) | Infrastructure, SIEM deployment, agent onboarding | ✅ Complete |
| Day 02 — Sysmon + Detection Rules | Detection engineering, MITRE ATT&CK mapping | 🔄 In progress |

---

## Current Lab State

| Component | Status |
|-----------|--------|
| Proxmox Host | ✅ Running |
| Ubuntu Server (wazuh_server) | ✅ Running |
| Wazuh SIEM | ✅ Running |
| Windows 11 Endpoint (win_endpoint_01) | ✅ Running |
| Wazuh Agent | ✅ Active |
| Event Collection | ✅ Validated |
| Threat Hunting | ✅ Validated |
| Sysmon | ⬜ Pending |
| Custom Detection Rules | ⬜ Pending |
| MITRE ATT&CK Mapping | ⬜ Pending |

---

## Day 01, Proxmox, Wazuh SIEM, and Windows Endpoint Setup

## Objective

Build the first stage of a practical detection and response homelab.

The goal was to deploy a dedicated virtualisation host, install Wazuh SIEM, create a Windows 11 endpoint, connect the endpoint to Wazuh, and confirm security events appear in the Wazuh Threat Hunting dashboard.

## Hardware

Lenovo ThinkCentre M710q Mini

Intel Core i5 7400T

16 GB RAM

256 GB SSD

Dedicated Ethernet connection to home router

## Architecture

```
Home Router
    │
    └── Proxmox VE Host (Lenovo ThinkCentre M710q)
            │
            ├── VM 100 — Ubuntu Server 24.04 LTS (wazuh_server)
            │       ├── Wazuh Manager
            │       ├── Wazuh Indexer
            │       └── Wazuh Dashboard
            │
            └── VM 101 — Windows 11 Pro (win_endpoint_01)
                    └── Wazuh Agent ──► reports to wazuh_server
```

## Phase 1, Proxmox Installation

Installed Proxmox VE on the Lenovo ThinkCentre using a bootable USB installer.

### BIOS Configuration

The first installation attempt returned a KVM virtualisation warning.

Cause:

Intel Virtualization Technology was disabled in BIOS.

Resolution:

Enabled Intel Virtualization Technology in Lenovo BIOS.

### Network Configuration

Configured Proxmox networking and confirmed access through the web dashboard.

Management interface:

vmbr0

Physical adapter:

enp0s31f6

The Proxmox host was connected directly to the home router for stable network access.

## Phase 2, Wazuh Server Deployment

Uploaded the Ubuntu Server 24.04 LTS ISO to Proxmox.

Created an Ubuntu Server VM with:

VM ID: 100

VM name: wazuh_server

CPU: 4 virtual cores

Memory: 8192 MB

Disk: 70 GB

Network adapter: VirtIO

Network bridge: vmbr0

### Storage Planning

Adjusted the Ubuntu logical volume during installation.

Final layout:

Root filesystem: 62 GB

Boot partition: 2 GB

Free LVM reserve: about 6 GB

This gives the Wazuh indexer enough usable storage for a small lab.

### Ubuntu Setup

Configured:

Hostname: wazuh_server

Username: jerin

SSH access: enabled

### Wazuh Installation

Installed the Wazuh all in one stack.

Components:

1. Wazuh manager
2. Wazuh indexer
3. Wazuh dashboard

Saved the Wazuh dashboard credentials in a private password manager.

## Phase 3, Windows Endpoint Deployment

Created a Windows 11 Pro VM with:

VM ID: 101

VM name: win_endpoint_01

CPU: 2 virtual cores

Memory: 4096 MB

Disk: 55 GB

BIOS: OVMF UEFI

TPM: version 2.0

Machine type: q35

Disk controller: VirtIO SCSI

Network adapter: VirtIO

Network bridge: vmbr0

### VirtIO Driver Installation

Windows Setup did not initially detect the virtual disk.

Cause:

The VirtIO SCSI storage driver was not available in the Windows installer.

Resolution:

Attached the VirtIO ISO as a second virtual CD drive.

Loaded the driver from:

vioscsi

w11

amd64

Installed the remaining VirtIO guest tools after Windows Setup completed.

## Phase 4, Wazuh Agent Enrollment

Installed the Wazuh Windows agent.

The first enrollment attempt failed.

### Troubleshooting

Reviewed the endpoint agent log:

C:\Program Files (x86)\ossec_agent\ossec.log

The Windows agent was pointing to the wrong Wazuh manager address.

Confirmed the correct Wazuh server address from Ubuntu.

Updated the Windows agent configuration.

Restarted the Wazuh agent service.

Confirmed successful enrollment.

### Final Status

Agent name: win_endpoint_01

Agent status: Active

## Phase 5, Event Validation

Opened the Wazuh dashboard.

Navigated to:

Agents management

Summary

Confirmed the Windows endpoint appeared as active.

Navigated to:

Threat Hunting

Events

Confirmed Windows endpoint activity appeared in the dashboard.

## Skills Demonstrated

1. Bare metal Proxmox VE deployment
2. BIOS virtualisation troubleshooting
3. Proxmox networking
4. Linux bridge configuration
5. Ubuntu Server VM deployment
6. Linux LVM storage planning
7. Wazuh SIEM deployment
8. Windows 11 Pro VM deployment
9. VirtIO storage driver installation
10. VirtIO network driver installation
11. Wazuh agent installation
12. Wazuh agent enrollment
13. Endpoint log review
14. Network troubleshooting
15. SIEM event validation
16. Threat Hunting dashboard review

## Issues Resolved

### Issue 1, KVM Virtualisation Warning

Cause:

Intel Virtualization Technology was disabled.

Resolution:

Enabled the BIOS setting.

### Issue 2, Unsupported Ubuntu Version

Cause:

The first Ubuntu VM used Ubuntu 26.04.

Resolution:

Rebuilt the VM using Ubuntu Server 24.04 LTS.

### Issue 3, Windows Installer Could Not See Disk

Cause:

VirtIO SCSI driver was missing.

Resolution:

Attached the VirtIO ISO and loaded the storage driver.

### Issue 4, Wazuh Agent Enrollment Failed

Cause:

The endpoint agent pointed to the wrong manager address.

Resolution:

Reviewed the agent log, corrected the Wazuh server address, restarted the agent service, and confirmed successful enrollment.

## Next Steps

1. Install Sysmon
2. Configure Wazuh Sysmon collection
3. Generate test activity
4. Validate Sysmon events in Threat Hunting
5. Create failed Windows logon detection
6. Create suspicious PowerShell detection
7. Create local administrator activity detection
8. Add MITRE ATT&CK mapping
9. Add screenshots
