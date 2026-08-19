# LinkedIn Post

I built a Web Application Firewall monitoring environment for a simulated banking environment — **AtlasBank**.

The question behind the project was:

> A WAF can detect an attack. But can the security team actually see, investigate, and measure what happened?

I built the pipeline:

**Kali Linux → pfSense → Nginx → ModSecurity + OWASP CRS → Security Logs → Splunk → SOC Dashboard**

The supplied Splunk environment contained telemetry from ModSecurity, Nginx, Sysmon, Windows Security, Windows System, Windows Application, and IIS.

Across the supplied data, I recorded **218,604 telemetry events** — not 218,604 attacks.

The `AtlasBank WAF Monitoring` dashboard provides visibility into:

- Detected web attacks over time
- Security event sources
- Event distribution
- Recent ModSecurity events

One important finding was a firewall visibility gap: controlled reconnaissance against pfSense was not represented in the existing Splunk data inventory.

That led to an important lesson:

**A security control is only part of the solution. Logging, detection, investigation, and response have to work together.**

My methodology is:

**Build → Attack → Detect → Investigate → Fix → Re-test → Document**

Next, I am evolving Atlas Core from Splunk to Wazuh and expanding monitoring to Active Directory, Windows endpoints, Sysmon, pfSense, Nginx, ModSecurity, authentication activity, and incident response.

The long-term objective is to simulate the enterprise security lifecycle:

**Attack → Detection → Investigation → Containment → Recovery → Hardening**

#CyberSecurity #SOC #SIEM #AppSec #WAF #DetectionEngineering #BlueTeam #RedTeam #Splunk #Wazuh #ActiveDirectory #CyberSecurityLab
