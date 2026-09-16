# Detection: Repeated Failed Administrator Logons

## Overview

This detection identifies repeated failed authentication attempts involving the Windows Administrator account.

The detection uses Windows Security Event ID 4625 and is intended to help identify possible brute-force or password-guessing activity.

## Data Source

- Log Source: Windows Security Event Log
- Event ID: `4625`
- SIEM: Splunk Enterprise
- Endpoint: Windows 10

## Splunk Detection

```spl
index=* host="DESKTOP-681O1RG" EventCode=4625 Account_Name="Administrator"
| eval Detection="Repeated Failed Administrator Logons"
| eval Severity="Medium"
| table _time host Account_Name Account_Domain Failure_Reason Status Sub_Status Logon_Type Caller_Process_Name Source_Network_Address Severity Detection
| sort - _time