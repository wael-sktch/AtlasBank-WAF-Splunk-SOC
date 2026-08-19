# AtlasBank WAF Monitoring — Findings

| ID | Finding | Severity | Status |
|---|---|---|---|
| WAF-001 | Centralized WAF visibility implemented | Informational | Closed |
| WAF-002 | WAF monitoring dashboard implemented | Informational | Closed |
| WAF-003 | Multi-layer telemetry requires normalization/prioritization | Medium | Open |
| WAF-004 | Firewall telemetry absent from current Splunk inventory | Medium | Open |
| WAF-005 | Telemetry should be verified before aggressive testing | Medium | Process improvement |

## WAF-001 — Centralized WAF Visibility

ModSecurity audit events were successfully ingested into Splunk.

Evidence:

```text
sourcetype=modsecurity
source=/var/log/nginx/modsec_audit.log
```

**Recommendation:** retain centralized collection and create structured detections.

## WAF-002 — WAF Monitoring Dashboard

The `AtlasBank WAF Monitoring` dashboard provides visibility into detected web attacks, event sources, event distribution, and recent events.

**Recommendation:** continue developing the dashboard into a SOC investigation view.

## WAF-003 — Telemetry Volume Requires Prioritization

The environment contains 218,604 supplied events. Volume demonstrates collection, but useful detection requires normalization, context, severity, and correlation.

**Recommendation:** map source IP, destination, URI, HTTP method, rule ID, action, severity, and attack category where available.

## WAF-004 — Firewall Telemetry Gap

Controlled reconnaissance from Kali (`10.10.40.10`) against pfSense (`10.10.40.1`) reached services, while the existing Splunk inventory did not contain a dedicated firewall sourcetype.

**Recommendation:** forward pfSense logs to the monitoring platform and validate the complete path:

```text
Kali -> pfSense -> Syslog -> SIEM -> Detection
```

## WAF-005 — Telemetry-First Testing

Security testing should not begin with destructive activity before the monitoring pipeline is confirmed.

Required sequence:

```text
Verify logging -> Verify ingestion -> Generate controlled event -> Confirm detection -> Broader testing
```
