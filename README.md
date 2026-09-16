# SOC Incident Detection, Investigation & Response Lab

A hands-on Security Operations Center (SOC) lab focused on Windows security monitoring, threat detection, alert investigation, and incident response using Splunk, Sysmon, and MITRE ATT&CK.

## Project Objective

This project simulates a small SOC environment where Windows endpoint telemetry is collected, analyzed, and used to detect suspicious activity.

The project demonstrates a practical SOC workflow:

**Collect → Detect → Investigate → Map → Document → Respond**

## Lab Environment

| Component | Technology |
|---|---|
| SIEM | Splunk Enterprise |
| Endpoint | Windows 10 |
| Endpoint Telemetry | Sysmon |
| Log Collection | Splunk Universal Forwarder |
| Server | Windows Server |
| Virtualization | VirtualBox |
| Threat Framework | MITRE ATT&CK |

## Detection Use Cases

### 1. Repeated Failed Administrator Logons

- Windows Security Event ID: `4625`
- Detection focus: Failed Administrator authentication attempts
- MITRE ATT&CK: `T1110 — Brute Force`
- Investigation: Account, failure reason, status codes, logon type, source address, and caller process

### 2. Suspicious PowerShell Execution

- Sysmon Event ID: `1`
- Detection focus: PowerShell execution containing `ExecutionPolicy` or `Bypass`
- MITRE ATT&CK: `T1059.001 — PowerShell`
- Investigation: User, command line, process image, and parent process

### 3. Suspicious Command-Line Activity

- Sysmon Event ID: `1`
- Detection focus: Selected Windows command-line activity
- MITRE ATT&CK: `T1059.003 — Windows Command Shell`
- Investigation: User, command line, process image, and parent process

## SOC Investigation Workflow

```text
Windows Endpoint
       |
       v
Windows Security Logs + Sysmon
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
Scheduled Alerts
       |
       v
Alert Triage & Investigation
       |
       v
MITRE ATT&CK Mapping
       |
       v
Incident Documentation
```

## SOC Dashboard

The project includes a Splunk dashboard covering:

- Failed Administrator Logons
- Suspicious PowerShell Execution
- Suspicious Command-Line Activity
- Last 24 hours monitoring

Dashboard evidence is available in the `screenshots` directory.

## Repository Structure

```text
├── README.md
├── detections/
│   ├── failed-administrator-logons.md
│   ├── suspicious-powershell.md
│   └── suspicious-command-line.md
├── docs/
│   ├── lab-architecture.md
│   ├── mitre-attack-mapping.md
│   └── incident-reports/
│       ├── incident-report-01-failed-admin-logons.md
│       └── incident-report-02-suspicious-powershell.md
├── screenshots/
└── spl/
    ├── failed-admin-logons.spl
    ├── suspicious-powershell.spl
    └── suspicious-command-line.spl
```

## Skills Demonstrated

- Splunk SIEM
- SPL detection queries
- Windows Security Event Analysis
- Sysmon telemetry analysis
- Alert triage
- Process and command-line investigation
- Detection engineering
- MITRE ATT&CK mapping
- Incident documentation
- SOC dashboard development

## Project Deliverables

- 3 SOC detection use cases
- 3 Splunk detection queries
- Scheduled Splunk alerts
- MITRE ATT&CK mapping
- 2 incident investigation reports
- SOC monitoring dashboard
- Investigation evidence screenshots
- Lab architecture documentation

## Lab Disclaimer

This project was conducted in an isolated virtual lab environment using controlled test activity.

The simulated events were created for cybersecurity learning, detection engineering, and SOC investigation practice. The presence of a detection does not by itself establish malicious activity or a confirmed compromise.
