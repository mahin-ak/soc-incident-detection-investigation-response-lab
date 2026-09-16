# Incident Report 02 — Suspicious PowerShell Execution

## 1. Executive Summary

A Splunk detection for suspicious PowerShell execution was investigated using Sysmon Process Create telemetry.

The investigation identified PowerShell execution containing the `-ExecutionPolicy Bypass` argument. The event was reviewed using the user, process image, command line, parent process, and execution context.

The activity was generated as a controlled test within the SOC lab to validate detection and investigation workflows. It does not establish a confirmed malicious PowerShell execution.

## 2. Alert Details

**Alert Name:** SOC - Suspicious PowerShell Execution

**Severity:** High

**Data Source:** Sysmon

**Event ID:** `1` — Process Create

**Affected Host:** `DESKTOP-681O1RG`

**User:** `MAHIN\Administrator`

**MITRE ATT&CK:** `T1059.001 — Command and Scripting Interpreter: PowerShell`

## 3. Evidence Observed

The controlled test generated a Sysmon Process Create event with the following characteristics:

| Field | Observed Value |
|---|---|
| Event ID | `1` |
| Host | `DESKTOP-681O1RG` |
| User | `MAHIN\Administrator` |
| Process | `powershell.exe` |
| Execution Policy | `Bypass` |
| Parent Process | `cmd.exe` |

The test command included:

```text
-NoProfile -ExecutionPolicy Bypass -Command "Write-Output 'SOC_SUSPICIOUS_POWERSHELL_TEST'"