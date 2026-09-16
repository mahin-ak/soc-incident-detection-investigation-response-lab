# Incident Report 01 — Repeated Failed Administrator Logons

## 1. Executive Summary

A detection for repeated failed authentication attempts against the Windows Administrator account was investigated in the SOC lab.

The investigation identified multiple Windows Security Event ID 4625 events. The events showed failed authentication attempts with the failure reason "Unknown user name or bad password."

The activity occurred within a controlled virtual lab environment and was generated for detection and investigation practice. The evidence does not establish that the activity was a real malicious attack.

## 2. Alert Details

**Alert Name:** Repeated Failed Administrator Logons

**Severity:** Medium

**Data Source:** Windows Security Event Log

**Event ID:** `4625`

**Affected Host:** `DESKTOP-681O1RG`

**Account:** `Administrator`

**MITRE ATT&CK:** `T1110 — Brute Force`

## 3. Evidence Observed

The investigation returned six failed authentication events involving the Administrator account.

Key observed values included:

| Field | Observed Value |
|---|---|
| Event ID | `4625` |
| Account | `Administrator` |
| Failure Reason | Unknown user name or bad password |
| Status | `0xC000006D` |
| Sub-Status | `0xC000006A` |
| Logon Type | `2` |
| Caller Process | `C:\Windows\System32\svchost.exe` |
| Source Address | `::1` |

The `::1` address is the IPv6 loopback address and indicates local-host activity in this lab scenario.

## 4. Investigation & Analysis

The analyst reviewed the authentication failure fields, account information, logon type, caller process, and source address.

The events targeted the Windows Administrator account and contained authentication failure status codes consistent with an invalid username or password condition.

The source address was `::1`, which indicates the activity originated locally rather than from a remote network address in this lab scenario.

The activity was treated as a controlled lab simulation. No conclusion of confirmed compromise was made based solely on these events.

## 5. MITRE ATT&CK Mapping

**Technique:** `T1110 — Brute Force`

**Tactic:** Credential Access

Repeated failed authentication attempts can be relevant to brute-force or password-guessing investigations. Additional context is required before classifying activity as malicious.

## 6. Response Considerations

For a production environment, an analyst should:

1. Validate whether the authentication attempts were expected.
2. Identify the affected account and host.
3. Review the source address and authentication type.
4. Search for additional failed and successful authentication events.
5. Correlate the activity with other endpoint and network telemetry.
6. Determine whether account protection or containment actions are required.
7. Document and escalate the incident according to organizational procedures.

## 7. Remediation Recommendations

Recommended defensive measures include:

- Use strong, unique passwords for privileged accounts.
- Avoid unnecessary use of built-in Administrator accounts.
- Monitor repeated authentication failures.
- Apply account protection and lockout policies where appropriate.
- Restrict unnecessary administrative access.
- Correlate authentication events with endpoint telemetry.

## 8. Conclusion

The investigation successfully demonstrated detection and triage of repeated failed Administrator authentication attempts using Windows Security Event ID 4625 and Splunk.

The observed activity was part of a controlled SOC lab environment. The investigation demonstrates how an analyst can collect evidence, assess authentication context, map activity to MITRE ATT&CK, and document response considerations.

## 9. Evidence

Supporting Splunk investigation evidence is available in the repository:

- `screenshots/06-failed-logon-investigation.png`
- `spl/failed-admin-logons.spl`
- `detections/failed-administrator-logons.md`