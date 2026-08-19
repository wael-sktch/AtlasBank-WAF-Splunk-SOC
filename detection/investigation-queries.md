# Splunk Investigation Queries

> Replace `index=*` with the dedicated AtlasBank security index if one is configured.

## Event Source Inventory

```spl
index=*
| stats count by sourcetype
| sort - count
