# MITRE ATT&CK Mapping

This document maps the SOC detection use cases developed in this lab to the relevant MITRE ATT&CK techniques.

## Detection Mapping

| Detection | Data Source | Event | MITRE ATT&CK Technique | Tactic |
|---|---|---|---|---|
| Repeated Failed Administrator Logons | Windows Security | Event ID 4625 | T1110 — Brute Force | Credential Access |
| Suspicious PowerShell Execution | Sysmon | Event ID 1 | T1059.001 — PowerShell | Execution |
| Suspicious Command-Line Activity | Sysmon | Event ID 1 | T1059.003 — Windows Command Shell | Execution |

---

## 1. T1110 — Brute Force

### Detection

**Repeated Failed Administrator Logons**

The detection monitors Windows Event ID 4625 for failed authentication attempts involving the Administrator account.

### Relevant Telemetry

- Windows Security Event ID: `4625`
- Account: `Administrator`
- Failure reason: Unknown user name or bad password
- Status: `0xC000006D`
- Sub-Status: `0xC000006A`

### Investigation Context

Repeated authentication failures can be associated with password-guessing activity. Analysts should review the source address, authentication type, account, timing, and surrounding events before determining whether the activity is suspicious.

---

## 2. T1059.001 — PowerShell

### Detection

**Suspicious PowerShell Execution**

The detection monitors Sysmon Process Create events for PowerShell commands containing `ExecutionPolicy` or `Bypass`.

### Relevant Telemetry

- Sysmon Event ID: `1`
- Process: `powershell.exe`
- Command-line arguments
- User
- Parent process

### Investigation Context

PowerShell is a legitimate Windows administration tool. The presence of `ExecutionPolicy Bypass` can warrant additional investigation, but it does not independently prove malicious activity.

Analysts should review the complete command line, parent process, user, timing, and related endpoint activity.

---

## 3. T1059.003 — Windows Command Shell

### Detection

**Suspicious Command-Line Activity**

The detection monitors Sysmon Process Create events for selected Windows command-line activity.

### Relevant Telemetry

- Sysmon Event ID: `1`
- Process: `cmd.exe`
- Command line
- User
- Parent process

### Investigation Context

The lab used `whoami` as a controlled test command to validate detection and investigation workflows.

Command-line activity should be evaluated in context because administrative and security tools commonly use Windows command shell functionality.

---

## Detection Engineering Summary

The lab demonstrates how endpoint telemetry can be mapped to MITRE ATT&CK techniques to provide additional context during SOC alert triage.

The three detections cover:

- Credential Access
- Execution
- PowerShell activity
- Windows Command Shell activity

All events used for validation were generated within a controlled virtual lab environment.