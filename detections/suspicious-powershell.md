# Detection: Suspicious PowerShell Execution

## Overview

This detection identifies PowerShell execution using `ExecutionPolicy Bypass`.

PowerShell is a legitimate Windows administration tool, but execution with policy bypass can warrant additional investigation depending on the surrounding context.

## Data Source

- Log Source: Sysmon
- Event ID: `1` — Process Create
- SIEM: Splunk Enterprise
- Endpoint: Windows 10

## Splunk Detection

```spl
index=sysmon EventCode=1
| search Image="*powershell.exe"
| search CommandLine="*ExecutionPolicy*" OR CommandLine="*Bypass*"
| eval Severity="High"
| eval Detection="Suspicious PowerShell Execution"
| table _time host User Image CommandLine ParentImage ParentCommandLine Severity Detection
| sort - _time