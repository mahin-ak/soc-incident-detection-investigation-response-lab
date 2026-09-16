# SOC Incident Detection, Investigation & Response Lab

A hands-on Security Operations Center (SOC) lab focused on Windows security monitoring, threat detection, alert investigation, and incident response using Splunk, Sysmon, and MITRE ATT&CK.

## Project Overview

This project simulates a small SOC environment where Windows security and Sysmon telemetry are collected, analyzed, and used to detect suspicious activity.

The lab demonstrates practical SOC workflows including:

- Security event collection and monitoring
- SIEM-based alert detection
- Alert investigation and triage
- True-positive / false-positive analysis
- MITRE ATT&CK mapping
- Incident documentation
- Detection engineering
- SOC dashboard creation

## Lab Environment

| Component | Technology |
|---|---|
| SIEM | Splunk Enterprise |
| Endpoint Telemetry | Sysmon |
| Log Collection | Splunk Universal Forwarder |
| Endpoint | Windows 10 |
| SIEM Server | Windows Server |
| Virtualization | VirtualBox |
| Threat Framework | MITRE ATT&CK |

## Detection Use Cases

### 1. Repeated Failed Administrator Logons

- Windows Event ID: `4625`
- Detection: Repeated failed Administrator authentication attempts
- MITRE ATT&CK: `T1110 - Brute Force`
- Investigation includes authentication status, logon type, source address, and caller process.

### 2. Suspicious PowerShell Execution

- Sysmon Event ID: `1`
- Detection: PowerShell execution using `ExecutionPolicy Bypass`
- MITRE ATT&CK: `T1059.001 - PowerShell`
- Investigation includes command line, user, parent process, and execution context.

### 3. Suspicious Command-Line Activity

- Sysmon Event ID: `1`
- Detection: Suspicious Windows command-shell activity
- MITRE ATT&CK: `T1059.003 - Windows Command Shell`
- Investigation includes command line, process, user, and parent process.

## SOC Workflow

```text
Windows Endpoint
       |
       v
Sysmon / Windows Security Logs
       |
       v
Splunk Universal Forwarder
       |
       v
Splunk Enterprise SIEM
       |
       v
Detection Rules
       |
       v
Alert Investigation
       |
       v
MITRE ATT&CK Mapping
       |
       v
Incident Documentation