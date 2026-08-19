
# AtlasBank Detection Engineering

## Purpose

This directory documents how AtlasBank security telemetry is converted into detections and investigation workflows.

The objective is not simply to collect logs.

The objective is:

Attack → Telemetry → Detection → Investigation → Response → Validation

---

## Detection Lifecycle

1. Identify the attack behavior.
2. Identify the telemetry source.
3. Determine which fields contain useful evidence.
4. Build an initial SPL query.
5. Test the query against known activity.
6. Reduce false positives.
7. Define severity and analyst action.
8. Document the detection.
9. Re-test after remediation.

---

## Current Telemetry

Primary sources include:

- ModSecurity
- Nginx access logs
- Nginx error logs
- Windows Security
- Windows System
- Windows Application
- Sysmon
- IIS

---

## Current Detection Priorities

| Detection | Source | Priority |
|---|---|---|
| WAF rule activity | ModSecurity | High |
| Web attack spikes | ModSecurity/Nginx | High |
| Suspicious HTTP requests | Nginx | High |
| Authentication anomalies | Windows Security | High |
| Suspicious process activity | Sysmon | High |
| Firewall reconnaissance | pfSense | High |
| Web server errors | Nginx | Medium |

---

## Analyst Workflow

```text
Alert
  ↓
Identify source
  ↓
Validate timestamp
  ↓
Identify source IP
  ↓
Identify target
  ↓
Review request/activity
  ↓
Correlate related events
  ↓
Determine attack category
  ↓
Assess impact
  ↓
Contain / remediate
  ↓
Re-test
