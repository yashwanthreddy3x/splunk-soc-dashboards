**SOC Dashboards – Splunk (SSH & Web Threat Detection)
**
This project demonstrates hands-on SIEM experience using Splunk to detect and investigate SSH brute-force attempts, suspicious web traffic, and attacker behaviors. The dashboards provide actionable insights for SOC analysts during real-time threat monitoring and incident response.

**Key Capabilities
**
Continuous monitoring of SSH authentication (failed/successful logins, sudo misuse, abnormal login spikes)

Automated brute-force detection based on IP frequency, login failures, and time thresholds

Apache web access analysis to spot malicious URIs, enumeration attempts, and bot scraping behaviors

Geo-mapping attacker IPs to trace global threat origins and identify high-risk regions

Time-based event correlation to support evidence collection and forensic investigation

IOC-based pivoting to quickly investigate suspicious activity

**Use Cases
**
Detect SSH brute-force attacks

Identify credential guessing attempts

Track enumeration of admin directories/web endpoints

Trace suspicious incoming traffic sources

Support incident reporting with dashboard-backed evidence

** Dashboard Panels (What You Can See)
**
**SSH Dashboard:
**
Failed vs Successful login charts

Login anomaly patterns (sudden spikes)

Username-based incorrect logins

Source IP aggregation and ranking

Alert conditions for brute-force patterns

Command execution monitoring with sudo tracking

**Apache Web Dashboard:
**
Suspicious URI access (admin panels, shell paths, probing attempts)

HTTP error anomaly mapping (403, 404, 500 trends)

Most frequent IP sources

Request method abuse (GET/POST noise)

Geo-location mapping of attacker IPs

**Repository Structure
**
splunk-soc-dashboards/
│
├── dashboards/          # Splunk dashboard screenshots (SSH, Apache, attack maps)
├── spl_queries/         # SPL queries for detection, anomaly tracking, investigation
├── sample_logs/         # Sample SSH & Apache logs (sanitized for learning)
└── documentation/       # (Optional) Attack timeline reports, case study PDFs

**Example SPL Queries
**
**SSH Failed Login Overview
**
index=linux_logs sourcetype=ssh_logs action=failure
| stats count by src_ip, user, host
| sort -count


**SSH Brute-Force Detection
**
index=linux_logs sourcetype=ssh_logs action=failure
| bucket _time span=5m
| stats count by src_ip, user, _time
| where count > 10
| sort -count


**Apache Suspicious URI Monitoring
**
index=web_logs sourcetype=apache_access
| search uri_path="*/wp-admin*" OR uri_path="*/shell*" OR status=404
| stats count by src_ip, uri_path, status
| sort -count


**Apache Error Frequency Analysis
**
index=web_logs sourcetype=apache_error
| stats count by status, host
| sort -count

**SOC Workflow Diagram
**
Log Collection (SSH + Apache)
       ↓
Splunk Indexing
       ↓
Dashboard Visualization & Alerting
       ↓
Incident Investigation & IOC Pivoting
       ↓
Evidence Reporting & Response

**Outcome & Purpose
**
This repository highlights hands-on cybersecurity experience including:

SIEM operations (Splunk)

Alert tuning and detection logic

SSH & web log investigation techniques

Threat hunting methodology

Evidence-based incident reporting

Designed to demonstrate readiness for SOC Analyst, Blue Team, and Threat Detection roles.

**Author
**
Yashwanth Reddy
Cybersecurity SOC Analyst Aspirant | SIEM | Threat Hunting | Blue Team

**Notes
**
More dashboards, logs, and case study documentation will be added as the SOC environment evolves.
