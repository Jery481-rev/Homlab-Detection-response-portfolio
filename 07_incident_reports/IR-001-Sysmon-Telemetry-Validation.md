# IR-001 Discovery Activity Investigation

## Summary

Wazuh generated an alert for discovery activity executed on the Windows endpoint.

## Alert Details

Rule ID: 92031

Severity: Medium

Host: win-endpoint-01

## Investigation

Reviewed the process execution details.

The activity originated from PowerShell commands executed during Sysmon telemetry testing.

Commands included:

Get-Process

Get-Service

Get-LocalUser

No malicious activity was identified.

## MITRE ATT&CK

T1082 System Information Discovery

T1033 Account Discovery

## Outcome

Alert was determined to be expected lab activity.

Detection validated successfully.