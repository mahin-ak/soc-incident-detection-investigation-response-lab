# SOC Lab Architecture

## Overview

This lab uses a virtualized Windows environment to simulate a small Security Operations Center (SOC) monitoring architecture.

The environment consists of a Windows 10 endpoint, Sysmon for endpoint telemetry, Splunk Universal Forwarder for log collection, and Splunk Enterprise as the SIEM.

## Architecture

```text
+---------------------------+
|       Windows 10 VM       |
|                           |
|  Windows Security Logs    |
|  Sysmon Telemetry         |
+-------------+-------------+
              |
              | Splunk Universal Forwarder
              | TCP 9997
              v
+---------------------------+
|     Windows Server VM     |
|                           |
|     Splunk Enterprise     |
|          SIEM             |
+-------------+-------------+
              |
              v
+---------------------------+
| Detection & Investigation |
|                           |
|  SPL Detection Rules      |
|  Alert Triage             |
|  MITRE ATT&CK Mapping     |
|  Incident Reports         |
|  SOC Dashboard            |
+---------------------------+