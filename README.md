# Homelab Detection and Response Portfolio

Hands on blue team homelab built from bare metal. Each lab documents the full process from infrastructure deployment through detection engineering, threat hunting, and incident response.

## Overview

This repository demonstrates practical experience across:

* Proxmox Virtualisation
* Ubuntu Server Administration
* Wazuh SIEM
* Windows Endpoint Monitoring
* Sysmon Telemetry
* Threat Hunting
* Incident Response
* Detection Engineering
* MITRE ATT&CK Mapping

## Lab Architecture

```text
Home Router
    │
    └── Proxmox VE Host (Lenovo ThinkCentre M710q)
            │
            ├── VM 100 - Ubuntu Server 24.04 LTS
            │       ├── Wazuh Manager
            │       ├── Wazuh Indexer
            │       └── Wazuh Dashboard
            │
            └── VM 101 - Windows 11 Pro
                    ├── Sysmon
                    └── Wazuh Agent
```

## Lab Index

| Lab                                                                                                                          | Focus                                                          | Status     |
| ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- | ---------- |
| [Day 01 - Proxmox, Wazuh, Windows Endpoint Deployment](02_proxmox_build/day_01_proxmox_wazuh_windows_endpoint.md)            | Infrastructure, SIEM Deployment                                | ✅ Complete |
| [Day 02 - Sysmon Telemetry and Detection Validation](04_windows_endpoint_telemetry/Day_02_Sysmon_Telemetry_and_Detection.md) | Detection Engineering, MITRE ATT&CK Mapping, Incident Response | ✅ Complete |

## Investigation Reports

| Report                                                                                                                    | Focus                                            | Status     |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ | ---------- |
| [IR-002 - Failed Login Investigation](07_incident_reports/IR-002_Failed_Login_Investigation.md)                           | Credential Access, Brute Force Detection         | ✅ Complete |
| [IR-003 - Local Administrator Creation](07_incident_reports/IR-003_Local_Admin_Creation.md)                               | Persistence, Privilege Escalation                | ✅ Complete |
| [IR-004 - PowerShell Reconnaissance Investigation](07_incident_reports/IR-004_PowerShell_Reconnaissance_Investigation.md) | Discovery, PowerShell Monitoring, Threat Hunting | ✅ Complete |

## Latest Achievements

* Built a Proxmox based cybersecurity homelab
* Deployed Wazuh SIEM on Ubuntu Server 24.04
* Onboarded Windows 11 endpoint telemetry
* Integrated Sysmon event collection
* Performed threat hunting and alert validation
* Created incident reports covering authentication, privilege escalation, and reconnaissance activity
* Mapped detections to MITRE ATT&CK techniques

## Current Lab State

| Component                             | Status        |
| ------------------------------------- | ------------- |
| Proxmox Host                          | ✅ Running     |
| Ubuntu Server (wazuh_server)          | ✅ Running     |
| Wazuh SIEM                            | ✅ Running     |
| Windows 11 Endpoint (win_endpoint_01) | ✅ Running     |
| Wazuh Agent                           | ✅ Active      |
| Event Collection                      | ✅ Validated   |
| Threat Hunting                        | ✅ Validated   |
| Sysmon                                | ✅ Active      |
| MITRE ATT&CK Mapping                  | ✅ Implemented |
| Incident Reporting                    | ✅ Implemented |
| Custom Detection Rules                | ⬜ Pending     |
| Active Directory Integration          | ⬜ Planned     |
| Multiple Endpoint Monitoring          | ⬜ Planned     |
| Microsoft Sentinel Integration        | ⬜ Planned     |

## Skills Demonstrated

### Infrastructure

* Proxmox VE
* Ubuntu Server
* Virtual Networking
* Virtual Machine Management
* Storage Provisioning
* Linux Administration

### Security Operations

* Wazuh SIEM
* Sysmon
* Threat Hunting
* Alert Investigation
* Incident Reporting
* MITRE ATT&CK Mapping
* Log Analysis

### Detection Use Cases

* Failed Authentication Monitoring
* Local Administrator Creation Detection
* PowerShell Activity Monitoring
* Discovery Activity Detection
* Process Creation Monitoring

## Screenshots

Evidence and supporting screenshots are available in:

```text
10_screenshots
```

## Roadmap

### Phase 1 - Infrastructure

* Proxmox Deployment
* Ubuntu Server Deployment
* Wazuh SIEM Installation
* Windows Endpoint Onboarding

### Phase 2 - Detection Validation

* Sysmon Integration
* Event Collection Validation
* Threat Hunting Workflows
* Incident Reporting

### Phase 3 - Detection Engineering

* Custom Wazuh Rules
* PowerShell Detection Logic
* Failed Login Correlation Rules
* Administrator Account Monitoring

### Phase 4 - Enterprise Expansion

* Active Directory
* Multiple Windows Endpoints
* Linux Endpoint Monitoring
* Microsoft Sentinel Integration
* Identity Monitoring

## Repository Structure

```text
01_lab_architecture
02_proxmox_build
03_wazuh_siem_lab
04_windows_endpoint_telemetry
05_detection_rules
06_threat_hunting
07_incident_reports
08_response_playbooks
09_mitre_mapping
10_screenshots
```

## Disclaimer

This repository is a personal learning environment designed for security operations, threat hunting, and detection engineering practice.

All testing is performed within a controlled homelab environment. No production systems are involved.
