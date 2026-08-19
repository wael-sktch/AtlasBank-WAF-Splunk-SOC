# AtlasBank WAF & SOC Architecture

## 1. Objective

The AtlasBank security architecture demonstrates how an enterprise web application can be protected and monitored through multiple security layers.

The architecture combines:

- network security
- web-server security
- WAF protection
- centralized logging
- SIEM monitoring
- security investigation

---

# 2. Logical Architecture

```text
                         ATLAS CORE ENTERPRISE

                              Kali Linux
                           Controlled Attacker
                                  |
                                  |
                                  v
                           +-------------+
                           |   pfSense   |
                           |  Firewall   |
                           +------+------+
                                  |
                                  v
                           +-------------+
                           |    Nginx    |
                           | Reverse     |
                           | Proxy       |
                           +------+------+
                                  |
                                  v
                       +----------------------+
                       |    ModSecurity       |
                       |    + OWASP CRS       |
                       |       WAF            |
                       +----------+-----------+
                                  |
                                  v
                       +----------------------+
                       |      AtlasBank       |
                       |    Web Application   |
                       |       / API          |
                       +----------+-----------+
                                  |
                                  v
                            Security Logs
                                  |
                                  v
                         +----------------+
                         |     Splunk     |
                         |      SIEM      |
                         +-------+--------+
                                 |
                                 v
                         SOC Investigation
