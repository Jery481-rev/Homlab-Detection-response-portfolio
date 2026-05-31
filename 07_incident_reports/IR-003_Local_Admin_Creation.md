# IR-003: Local Administrator Account Creation Investigation

## Summary

Wazuh generated alerts following the creation of a new local Windows account and the addition of that account to the local Administrators group.

The activity was performed intentionally within the lab environment to validate Windows Security Event monitoring, Sysmon visibility, Wazuh alert generation, and SOC investigation procedures.

No malicious activity was identified.

---

## Alert Details

| Field       | Value                                |
| ----------- | ------------------------------------ |
| Incident ID | IR-003                               |
| Alert Type  | Local Administrator Account Creation |
| Host        | win-endpoint-01                      |
| Data Source | Windows Security Event Log           |
| SIEM        | Wazuh 4.14.5                         |
| Severity    | Medium                               |
| Status      | Closed, Lab Activity                 |

---

## Scenario

A new user account was created on the Windows endpoint and elevated to local administrator privileges.

Commands executed:

```powershell
net user socadmin Password123! /add

net localgroup administrators socadmin /add
```

The objective was to validate detection of account creation and privilege assignment events.

---

## Detection Source

Windows Security Events generated alerts relating to:

### User Account Creation

Event ID:

```text
4720
```

Description:

```text
A user account was created
```

### User Added to Local Administrators Group

Event ID:

```text
4732
```

Description:

```text
A member was added to a security enabled local group
```

---

## Investigation Steps

1. Opened Wazuh Threat Hunting.
2. Searched for the username:

```text
socadmin
```

3. Reviewed account creation events.
4. Reviewed local group membership modification events.
5. Correlated timestamps between both activities.
6. Confirmed the activity originated from the Windows endpoint.
7. Verified the actions matched the controlled lab exercise.

---

## Evidence Reviewed

| Evidence                      | Description                    |
| ----------------------------- | ------------------------------ |
| 21_user_account_created.png   | Account creation alert         |
| 22_admin_group_membership.png | Administrator group assignment |
| Wazuh Threat Hunting          | Event review and validation    |

---

## MITRE ATT&CK Mapping

| Tactic               | Technique      | ID        |
| -------------------- | -------------- | --------- |
| Persistence          | Create Account | T1136     |
| Persistence          | Local Account  | T1136.001 |
| Defense Evasion      | Valid Accounts | T1078     |
| Privilege Escalation | Valid Accounts | T1078     |

---

## Analysis

Creation of a new administrator account is a common persistence technique used by attackers after initial access.

Threat actors frequently create new accounts or add existing users to privileged groups to maintain access and perform administrative actions.

In this investigation, the activity was traced to controlled lab testing and matched the expected commands executed during validation.

No evidence of unauthorized access, malware activity, or persistence outside the planned exercise was identified.

---

## Impact Assessment

No production systems affected.

No unauthorized privilege escalation occurred.

No sensitive data was accessed.

No remediation required.

---

## Outcome

The investigation confirmed:

* Wazuh successfully detected account creation activity.
* Wazuh successfully detected administrator group membership changes.
* Windows Security Event monitoring is functioning correctly.
* The environment can detect persistence related account activity.

The alert was classified as expected lab activity.

---

## Recommended SOC Response

In a production environment:

1. Verify the account owner.
2. Confirm change approval.
3. Review the account creation source.
4. Check recent authentication activity.
5. Review other privileged group modifications.
6. Escalate unapproved administrator creation events immediately.

---

## Lessons Learned

Administrator account creation is a high value detection use case.

Monitoring Event IDs 4720 and 4732 provides visibility into persistence and privilege escalation activity.

Combining Windows Security Events with Wazuh alerting provides an effective method for identifying unauthorized account creation.
