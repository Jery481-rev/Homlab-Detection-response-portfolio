# IR-004: PowerShell Reconnaissance Investigation

## Summary

Wazuh generated multiple alerts following PowerShell based system enumeration activity on the Windows endpoint.

The activity was performed intentionally within the lab environment to validate Sysmon telemetry, Wazuh detection capabilities, and SOC investigation procedures.

No malicious activity was identified.

---

## Alert Details

| Field       | Value                              |
| ----------- | ---------------------------------- |
| Incident ID | IR-004                             |
| Alert Type  | PowerShell Reconnaissance Activity |
| Host        | win-endpoint-01                    |
| Data Source | Sysmon                             |
| SIEM        | Wazuh 4.14.5                       |
| Severity    | Medium                             |
| Status      | Closed, Lab Activity               |

---

## Scenario

PowerShell was used to enumerate system, user, service, and process information from the Windows endpoint.

Commands executed during the exercise:

```powershell
whoami

hostname

ipconfig /all

Get-Process

Get-Service

Get-LocalUser

Get-LocalGroup

net user

net localgroup administrators
```

The objective was to validate visibility of discovery activity within Wazuh and investigate the resulting alerts.

---

## Detection Source

Wazuh generated alerts associated with reconnaissance and discovery activity.

### Discovery Activity Executed

Rule ID:

92031

Description:

Discovery activity executed

### PowerShell Activity

Rule ID:

92021

Description:

PowerShell activity observed through Sysmon process creation events

### Process Chain Monitoring

Rule ID:

92066

Description:

PowerShell spawning additional Windows processes during enumeration

---

## Investigation Steps

1. Opened Wazuh Threat Hunting.
2. Filtered events for the Windows endpoint.
3. Reviewed Sysmon process creation events.
4. Examined PowerShell command execution details.
5. Reviewed parent and child process relationships.
6. Correlated alerts with the executed lab commands.
7. Verified no unauthorized activity occurred.

---

## Evidence Reviewed

| Evidence                              | Description               |
| ------------------------------------- | ------------------------- |
| 23_powershell_recon_alert.png         | PowerShell related alert  |
| 24_powershell_recon_event_details.png | Expanded event details    |
| Wazuh Threat Hunting                  | Alert review and analysis |

---

## MITRE ATT&CK Mapping

| Tactic    | Technique                              | ID        |
| --------- | -------------------------------------- | --------- |
| Discovery | System Information Discovery           | T1082     |
| Discovery | Account Discovery                      | T1033     |
| Execution | PowerShell                             | T1059.001 |
| Discovery | Process Discovery                      | T1057     |
| Discovery | System Network Configuration Discovery | T1016     |

---

## Analysis

PowerShell is commonly used by administrators for legitimate management tasks. It is also widely abused by attackers during post compromise activity.

The commands executed during this exercise performed reconnaissance against the local system and generated telemetry associated with discovery techniques.

Review of the event data confirmed the activity originated from the controlled lab environment and matched the commands executed during testing.

No evidence of persistence, lateral movement, privilege escalation, or malware execution was identified.

---

## Impact Assessment

No production systems affected.

No unauthorized access identified.

No sensitive data exposed.

No remediation required.

---

## Outcome

The investigation confirmed:

* Sysmon process creation events were successfully collected.
* Wazuh generated alerts for discovery activity.
* PowerShell execution monitoring is functioning correctly.
* Threat Hunting workflows can be used to investigate PowerShell activity.

The alert was classified as expected lab activity.

---

## Recommended SOC Response

In a production environment:

1. Review the executed PowerShell commands.
2. Verify the user who launched PowerShell.
3. Assess whether the activity aligns with approved administrative tasks.
4. Investigate any encoded or obfuscated commands.
5. Review related authentication and process events.
6. Escalate suspicious discovery activity for further investigation.

---

## Lessons Learned

PowerShell provides valuable visibility into endpoint activity when combined with Sysmon and Wazuh.

Monitoring discovery related commands helps identify reconnaissance activity often performed during the early stages of an attack.

Sysmon process creation events provide the context required to investigate PowerShell based detections effectively.
