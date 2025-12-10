# 🛡 SOC Dashboards – Splunk (SSH & Web Threat Detection)



This repository demonstrates hands-on SIEM experience using Splunk to detect and investigate SSH brute-force attempts, suspicious Apache web traffic, and attacker behaviors. The dashboards provide actionable threat intelligence for SOC analysts performing real-time monitoring, anomaly detection, and incident response.



---



## 🔍 Key Capabilities



- Monitor SSH authentication (successful/failed logins, abnormal login spikes, sudo usage)

- Detect SSH brute-force attacks using time-frequency thresholds and attacker IP analysis

- Analyze Apache HTTP logs to detect suspicious URIs, enumeration attempts, and error patterns

- Trace attacker IP origins globally using geo-location mapping

- Perform time-based correlation to support incident reporting and RCA

- Pivot investigations using IOC-based filtering for faster triage



---



## 🧩 Use Cases



✔ SSH brute-force detection  

✔ Enumeration and reconnaissance tracking (Apache)  

✔ Identifying malicious IP sources  

✔ Real-time monitoring for SOC alerting  

✔ Supporting evidence for incident reports  



---



## 📷 Dashboard Panels Overview



### 🔐 SSH Dashboard

- Failed vs Successful logins

- Source IP attack frequency trends

- Username anomalies and brute-force tracing

- Sudo misuse monitoring

- Time-series spike detection



### 🌐 Web Traffic (Apache) Dashboard

- Suspicious URI access detection (404/403 enumeration)

- HTTP status code error analytics

- Client IP request frequency monitoring

- Behavioral anomaly visualization

- Global attack source mapping



---



## 📁 Repository Structure


splunk-soc-dashboards/

│

├── dashboards/          # Splunk dashboard screenshots (SSH, Apache, Geo maps)

├── spl_queries/         # SPL queries for detection and analysis

├── sample_logs/         # Sanitized SSH & Apache log samples

└── documentation/       # (Optional) Case-study PDFs and SOC reports

---


## 🧪 Example SPL Queries

## 🟦 SSH Failed Login Overview

index=linux_logs sourcetype=ssh_logs action=failure

| stats count by src_ip, user, host

| sort -count



## 🟦 SSH Brute-force Attempt Detection

index=linux_logs sourcetype=ssh_logs action=failure

| bucket _time span=5m

| stats count by src_ip, user, _time

| where count > 10

| sort -count



## 🟦 Apache Suspicious URI Access

index=web_logs sourcetype=apache_access

| search uri_path="*/wp-admin*" OR uri_path="*/shell*" OR status=404

| stats count by src_ip, uri_path, status

| sort -count

---

## 🧭 SOC Workflow / Investigation Path

Logs (SSH + Apache)

↓

Splunk Indexing

↓

Dashboards + Alerts

↓

Analyst Investigation (Correlation + IOC Pivoting)

↓

Incident Documentation & Response

---

## 🎯 Project Purpose



- This project highlights practical SOC capabilities including:



- SIEM operations using Splunk



- Threat detection based on SSH and web logs



- Real-time dashboards for actionable insights



- Event correlation and anomaly spotting



- Blue Team methodology for incident response

---

## 🚀 Future Enhancements



- Automated alert notifications (Slack/Email integration)



- Threat intelligence enrichment (AbuseIPDB/OTX)



- MITRE ATT&CK mapping visualization



- Case-study PDFs under /documentation

---

## 🙌 Contribution



Suggestions, improvements, and pull requests are welcome!







