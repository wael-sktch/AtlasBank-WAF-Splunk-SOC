# ModSecurity Detection Engineering

## Objective

Detect suspicious web activity recorded by ModSecurity and make the events actionable for a SOC analyst.

## Telemetry

```text
Sourcetype:
modsecurity

Source:
 /var/log/nginx/modsec_audit.log
