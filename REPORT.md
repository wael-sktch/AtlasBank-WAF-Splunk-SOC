# AtlasBank WAF Monitoring & Web Attack Detection — Security Report

## Executive Summary

AtlasBank is a controlled banking application security laboratory. This phase evaluated whether web activity detected by ModSecurity could be centrally logged, searched, visualized, and investigated through Splunk.

The implemented pipeline was:

```text
Kali -> pfSense -> Nginx -> ModSecurity/OWASP CRS -> AtlasBank -> Logs -> Splunk
```

The supplied Splunk inventory contained **218,604 telemetry events** across eight sourcetypes. This is an event count, not an attack count.

The project successfully demonstrated centralized WAF visibility and dashboard-based monitoring. It also identified a firewall telemetry gap, leading to a telemetry-first methodology for future attack campaigns.

## Scope

- AtlasBank web application
- Nginx
- ModSecurity
- OWASP CRS
- Splunk
- Windows Security and Sysmon telemetry
- Controlled Kali testing
- pfSense visibility validation

## Key Results

1. ModSecurity audit events were visible in Splunk.
2. An `AtlasBank WAF Monitoring` dashboard was created.
3. Multiple security telemetry sources were centralized.
4. 218,604 supplied events were inventoried.
5. A firewall visibility gap was identified.
6. A telemetry-first testing process was established.

## Evidence Path

```text
Web Request
  -> ModSecurity
  -> modsec_audit.log
  -> Splunk ingestion
  -> Dashboard
  -> Analyst investigation
```

## Conclusion

The WAF monitoring phase is complete. The next maturity step is to migrate to Wazuh and expand visibility to Active Directory, Windows endpoints, Sysmon, pfSense, Nginx, ModSecurity, authentication activity, and incident response.
