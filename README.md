# Detection and Response Portfolio

## About

This repository documents my practical detection and response homelab work.

I currently work as an IT Support Engineer in a Microsoft focused environment. I am building deeper security operations skills through SIEM deployment, endpoint telemetry, log analysis, threat hunting, custom detection logic, MITRE ATT&CK mapping, incident documentation, and response playbooks.

## Current Lab Environment

The lab runs on a dedicated Lenovo ThinkCentre M710q Mini using Proxmox VE.

### Hardware

Lenovo ThinkCentre M710q Mini

Intel Core i5 7400T

16 GB RAM

256 GB SSD

### Current Architecture

Home router

Lenovo ThinkCentre running Proxmox VE

Ubuntu Server 24.04 LTS VM running Wazuh SIEM

Windows 11 Pro VM running the Wazuh endpoint agent

### Current Components

1. Proxmox VE host
2. Ubuntu Server 24.04 LTS
3. Wazuh manager
4. Wazuh indexer
5. Wazuh dashboard
6. Windows 11 Pro endpoint
7. Wazuh Windows agent
8. Windows security event collection
9. Wazuh Threat Hunting event validation

## Completed Work

1. Installed Proxmox VE on dedicated hardware
2. Enabled Intel Virtualization Technology in BIOS
3. Configured Proxmox networking
4. Created Ubuntu Server VM
5. Installed Wazuh SIEM
6. Created Windows 11 Pro endpoint VM
7. Installed VirtIO storage and network drivers
8. Installed and enrolled the Wazuh Windows agent
9. Confirmed Windows endpoint events appear in Wazuh Threat Hunting

## In Progress

1. Install Sysmon on the Windows endpoint
2. Collect Sysmon Operational events in Wazuh
3. Generate controlled Windows activity
4. Create the first custom detection rule

## Planned Detections

1. Multiple failed Windows logons
2. Suspicious PowerShell execution
3. New local administrator activity
4. Repeated SSH failed logins
5. Suspicious web server activity

## Planned Portfolio Work

1. Add Linux endpoint monitoring
2. Add Sysmon telemetry
3. Write threat hunting notes
4. Write incident reports
5. Write response playbooks
6. Map detections to MITRE ATT&CK
7. Add Microsoft Sentinel detections
8. Add Entra ID identity security projects

## Target Roles

1. Junior Detection and Response Engineer
2. SOC Analyst
3. Cyber Security Analyst
4. Junior Detection Engineer
5. Security Operations Analyst

## Skills Demonstrated

1. Virtualisation
2. SIEM deployment
3. Endpoint onboarding
4. Windows event collection
5. Network troubleshooting
6. Agent enrollment troubleshooting
7. Threat Hunting event review
8. Technical documentation
9. Detection engineering fundamentals

## Security and Privacy

All screenshots are reviewed before upload.

Passwords, recovery keys, MAC addresses, email addresses, and sensitive configuration details are removed or blurred.
