# AtlasBank WAF Monitoring & Web Attack Detection

## Overview

AtlasBank is a controlled enterprise banking security lab used to study how web attacks are detected, logged, investigated, and documented.

This phase focuses on **WAF monitoring and SIEM visibility** using Kali Linux, Nginx, ModSecurity + OWASP CRS, and Splunk.

> **Security question:** If a WAF detects an attack, can the security team actually see, investigate, and measure what happened?

## Architecture

```text
Kali Linux
    |
    v
 pfSense
    |
    v
 Nginx
    |
    v
ModSecurity + OWASP CRS
    |
    v
AtlasBank Web App
    |
    v
Security Logs
    |
    v
 Splunk
    |
    v
AtlasBank WAF Monitoring Dashboard
```

## Telemetry Inventory

| Sourcetype | Events |
|---|---:|
| `modsecurity` | 65,138 |
| `WinEventLog:Security` | 63,596 |
| `nginx_access` | 32,362 |
| `XmlWinEventLog:Microsoft-Windows-Sysmon/Operational` | 29,561 |
| `nginx_error` | 14,837 |
| `WinEventLog:System` | 10,595 |
| `WinEventLog:Application` | 2,381 |
| `iis` | 134 |
| **Total** | **218,604** |

> These are telemetry events, not 218,604 attacks.

## Dashboard

**AtlasBank WAF Monitoring** contains:

- Detected Web Attacks
- Security Event Sources
- Event Distribution
- Recent Security Events

Representative event:

```text
2026-08-09 07:45:23
sourcetype: modsecurity
source: /var/log/nginx/modsec_audit.log
```

## Findings

### WAF-001 — Centralized WAF visibility
**Status:** Closed

ModSecurity audit events were successfully collected into Splunk.

### WAF-002 — WAF monitoring dashboard
**Status:** Closed

A dashboard was created to visualize web attack activity and security telemetry.

### WAF-003 — Telemetry volume requires prioritization
**Severity:** Medium
**Status:** Open

218,604 events were observed across the supplied sources. High-volume telemetry should be normalized, prioritized, and correlated.

### WAF-004 — Firewall telemetry gap
**Severity:** Medium
**Status:** Open / next phase

Controlled reconnaissance against pfSense was not represented in the existing Splunk sourcetypes. Firewall logging must be integrated and validated.

### WAF-005 — Telemetry-first testing
**Severity:** Medium
**Status:** Process improvement

Before aggressive testing, verify logging, transport, SIEM ingestion, and detection with a controlled event.

## Investigation Method

```text
ATTACK
  |
RAW EVENT
  |
NORMALIZATION
  |
DETECTION
  |
ALERT
  |
INVESTIGATION
  |
RESPONSE
  |
RE-TEST
```

## Splunk Queries

```spl
index=* | stats count by sourcetype | sort - count
```

```spl
index=* sourcetype=modsecurity | timechart span=1h count
```

```spl
index=* earliest=-15m | table _time sourcetype source host _raw | sort _time
```

## Evidence

Before publishing screenshots or raw logs, remove credentials, tokens, cookies, secrets, and sensitive personal information.

See `evidence/README.md`.

## Project Status

- **Phase 1 — Splunk WAF Monitoring:** Completed
- **Phase 2 — Wazuh SOC Migration:** Planned
- **Phase 3 — AD Attack & Detection:** Planned
- **Phase 4 — Firewall Security Assessment:** Planned
- **Phase 5 — Full Attack Chain:** Planned
- **Phase 6 — Incident Response & Disaster Recovery:** Planned

## Methodology

**Build → Validate → Attack → Detect → Investigate → Fix → Re-test → Document**
