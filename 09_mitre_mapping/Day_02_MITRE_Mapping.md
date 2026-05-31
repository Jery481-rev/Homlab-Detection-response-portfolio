# Day 02 MITRE ATT&CK Mapping

## Overview

This document maps detections generated during Sysmon telemetry validation to the MITRE ATT&CK framework.

## Detection 1: Discovery Activity Executed

### Wazuh Rule

Rule ID: 92031

### Description

Discovery activity executed from PowerShell.

### ATT&CK Mapping

| Technique                                     | ID        |
| --------------------------------------------- | --------- |
| System Information Discovery                  | T1082     |
| Account Discovery                             | T1033     |
| Command and Scripting Interpreter: PowerShell | T1059.001 |

### Evidence

IR-001_Discovery_Activity_Investigation.md

15_discovery_activity_expanded.png

---

## Detection 2: PowerShell Activity

### Wazuh Rule

Rule ID: 92021

### Description

PowerShell execution observed on the endpoint.

### ATT&CK Mapping

| Technique  | ID        |
| ---------- | --------- |
| PowerShell | T1059.001 |

---

## Detection 3: Process Chain Monitoring

### Wazuh Rule

Rule ID: 92066

### Description

SecEdit.exe launched from PowerShell.

### ATT&CK Mapping

| Technique                    | ID        |
| ---------------------------- | --------- |
| PowerShell                   | T1059.001 |
| System Information Discovery | T1082     |

---

## Lessons Learned

MITRE ATT&CK provides a consistent method to classify endpoint activity and detections.

Mapping detections to ATT&CK techniques improves investigation quality and communication during incident response.
