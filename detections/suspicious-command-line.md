# Detection: Suspicious Command-Line Activity

## Overview

This detection identifies selected Windows command-line activity that may require additional investigation.

For this lab, `whoami` execution was used as a controlled simulation to demonstrate command-line detection and investigation.

## Data Source

- Log Source: Sysmon
- Event ID: `1` — Process Create
- SIEM: Splunk Enterprise
- Endpoint: Windows 10

## Splunk Detection

```spl
index=sysmon EventCode=1
| search CommandLine="*whoami*"
| eval Severity="Medium"
| eval Detection="Suspicious Command-Line Activity"
| table _time host User Image CommandLine ParentImage ParentCommandLine Severity Detection
| sort - _time