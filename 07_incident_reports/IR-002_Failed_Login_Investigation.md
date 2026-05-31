# IR-002: Failed Login Investigation

## Summary

Wazuh generated an alert for failed authentication activity on the Windows endpoint.

The activity was created intentionally as part of a controlled lab test to validate Windows security log collection, Wazuh alerting, and basic SOC investigation workflow.

No malicious activity was identified.

## Alert Details

| Field | Value |
|------|------|
| Incident ID | IR-002 |
| Alert Type | Failed Windows login |
| Host | Win11-endpoint |
| Log Source | Windows Security Event Log |
| Event ID | 4625 |
| SIEM | Wazuh |
| Status | Closed, Lab Activity |

## Detection Source

The alert was generated from Windows Security Event ID 4625.

Event ID 4625 records failed logon attempts on Windows systems.

## Investigation Steps

1. Opened Wazuh Threat Hunting.
2. Filtered events for failed logon activity.
3. Reviewed the alert details.
4. Confirmed the affected endpoint.
5. Checked the target username.
6. Checked the source IP address.
7. Correlated the timestamp with the lab test activity.
8. Confirmed the failed login attempts were manually generated.

## Evidence Reviewed

| Evidence | Details |
|------|------|
| Wazuh alert | Failed login event visible in Threat Hunting |
| Endpoint | Win11-endpoint |
| Event ID | 4625 |
| Screenshot | 18_failed_login_alert_expanded.png |

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|------|------|------|
| Credential Access | Brute Force | T1110 |

## Analysis

The failed login activity matched the controlled test performed on the Windows endpoint.

The event did not show evidence of unauthorized access, lateral movement, persistence, malware execution, or privilege escalation.

The alert confirms Wazuh is receiving Windows Security logs and identifying authentication failures.

## Outcome

The alert was classified as expected lab activity.

The detection worked as intended.

No containment or remediation was required.

## Recommended SOC Response

In a real environment, the next steps would be:

1. Confirm whether the account owner attempted the login.
2. Check the number of failed attempts.
3. Review the source IP address.
4. Check for successful login after failures.
5. Review related events on the same host.
6. Disable or reset the account if activity appears malicious.
7. Escalate if multiple accounts or systems are affected.

## Lessons Learned

Failed login events provide useful early indicators of password guessing or brute force activity.

The key investigation points are username, source IP address, failure count, timestamp, and whether a successful login followed the failures.