# Nginx Evidence

## Purpose

This directory contains evidence from the AtlasBank Nginx web-server telemetry.

Nginx evidence is used to correlate HTTP activity with ModSecurity/WAF detections and identify patterns such as request spikes, repeated requests, suspicious sources, and web-server errors.

---

## Evidence Sources

| Evidence | Splunk Sourcetype | Purpose |
|---|---|---|
| Access logs | `nginx_access` | HTTP request activity |
| Error logs | `nginx_error` | Web-server errors and anomalies |

---

## Evidence Collection

The following evidence was collected from the AtlasBank Splunk environment:

1. Nginx request volume over time.
2. Top request sources.
3. Nginx error activity over time.
4. Correlation between Nginx activity and ModSecurity events.

---

## Investigation Queries

### Nginx Request Timeline

```spl
index=* sourcetype=nginx_access
| timechart span=1h count
