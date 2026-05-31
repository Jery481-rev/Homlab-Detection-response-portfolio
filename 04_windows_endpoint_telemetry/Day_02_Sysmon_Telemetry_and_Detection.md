# Day 02. Sysmon Telemetry Validation and Detection Analysis

## Objective

Validate Sysmon log ingestion from a Windows 11 endpoint into Wazuh and investigate security detections generated from endpoint activity.

## Lab Environment

### Infrastructure

| Component        | Details                 |
| ---------------- | ----------------------- |
| Hypervisor       | Proxmox VE 9            |
| SIEM             | Wazuh 4.14.5            |
| Server OS        | Ubuntu Server 24.04 LTS |
| Endpoint         | Windows 11 Pro          |
| Endpoint Agent   | Wazuh Agent 4.14.5      |
| Telemetry Source | Sysmon                  |

## Activities Performed

The Windows endpoint was monitored through the Wazuh agent with Sysmon enabled.

Several PowerShell and system discovery commands were executed to generate telemetry for validation purposes.

Commands executed included:

```powershell
Get-Process
Get-Service
Get-LocalUser
whoami
hostname
ipconfig
```

## Detection Results

Wazuh successfully received and processed Sysmon events from the Windows endpoint.

The following detections were observed:

### Discovery Activity Executed

Rule ID: 92031

Wazuh identified system discovery behaviour generated through PowerShell enumeration commands.

This activity aligns with adversary reconnaissance techniques commonly observed during the early stages of an attack.

### PowerShell Activity Detection

Rule ID: 92021

PowerShell activity was monitored and logged successfully.

Command execution details were available for investigation through the Wazuh dashboard.

### Parent Child Process Detection

Rule ID: 92066

Wazuh detected SecEdit.exe launched from PowerShell.

This detection demonstrates visibility into process relationships and execution chains.

### Service Configuration Changes

Rule ID: 61104

Service startup configuration modifications were identified and logged.

This confirms endpoint configuration monitoring is functioning correctly.

## MITRE ATT&CK Mapping

| Activity                     | Technique                         | MITRE ID  |
| ---------------------------- | --------------------------------- | --------- |
| System Discovery             | Discovery                         | T1082     |
| Account Discovery            | Discovery                         | T1033     |
| PowerShell Execution         | Command and Scripting Interpreter | T1059.001 |
| Process Execution Monitoring | Defense Evasion / Execution       | Various   |

## Investigation Summary

Telemetry generated from the Windows endpoint was successfully collected by Wazuh.

The SIEM produced multiple detections from normal administrative activity, demonstrating:

* Sysmon visibility
* Process creation monitoring
* PowerShell monitoring
* Parent child process analysis
* MITRE ATT&CK mapping

The lab confirmed that endpoint telemetry is operational and suitable for future detection engineering and threat hunting exercises.

## Evidence

See screenshots in:

```text
10_screenshots/
13_sysmon_detection_events.png
14_sysmon_event_details.png
```

## Lessons Learned

* Sysmon provides significantly richer telemetry than standard Windows logs.
* Wazuh detection rules generate actionable alerts from endpoint activity.
* Process creation events are essential for threat hunting and investigation.
* Parent child process relationships provide valuable context during analysis.

## Next Steps

* Create custom detection rules.
* Generate failed logon events.
* Simulate local administrator account creation.
* Implement PowerShell detection use cases.
* Produce incident reports mapped to MITRE ATT&CK.
