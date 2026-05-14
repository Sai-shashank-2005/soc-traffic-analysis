# SOC Traffic Analysis & Threat Detection Portfolio

## Overview

This repository documents hands-on Security Operations Center (SOC) investigations and detection engineering workflows. Utilizing **SIEM (Splunk)** and **Network Traffic Analysis (Wireshark)**, this lab environment simulates real-world incident response scenarios. 

The focus is on moving from raw telemetry to actionable intelligence—identifying malicious activity, validating threats through behavioral analysis, mapping to MITRE ATT&CK frameworks, and producing professional security incident reports.

---

## 🎯 Core Competencies Demonstrated

* **SIEM & Detection Engineering:** Log ingestion, raw data parsing using SPL (`rex`), and building behavior-based detection rules in Splunk.
* **Network Traffic Analysis:** Deep packet inspection (PCAP) to reconstruct attack chains, extract indicators of compromise (IoCs), and analyze malware behavior.
* **Log Analysis:** Correlating telemetry across Windows Event Logs, Sysmon, and Windows Firewall.
* **Threat Identification:** Distinguishing between benign and malicious traffic, including C2 beaconing, port scanning, and drive-by downloads.
* **Incident Reporting:** Developing structured, evidence-based SOC reports with detailed mitigation recommendations.

---

## 📂 Repository Structure & Case Studies

This portfolio is divided into two primary disciplines: SIEM-based detection and packet-level forensic analysis.

### 🔹 Splunk SIEM Detection

Focused on detecting anomalous behavior and attacker techniques using statistical and time-based analysis in Splunk.

| Case ID | Title | Description | MITRE Tactic |
| :--- | :--- | :--- | :--- |
| **Case 1** | [Port Scan Detection](./splunk-detection/case-1-port-scan-detection/report.md) | Detected and mapped automated reconnaissance activity targeting multiple Windows service ports (RPC, NetBIOS, SMB) via firewall log telemetry. | Discovery (T1046) |
| **Case 2** | [C2 Beaconing Detection](./splunk-detection/case-2-c2-beaconing-detection/report.md) | Identified command-and-control behavior by analyzing connection frequency, interval (~5s), and jitter from outbound firewall telemetry. | Command & Control (T1071.001) |

### 🔹 PCAP Network Analysis (Wireshark)

Focused on inspecting raw network traffic to extract malware payloads, identify C2 infrastructure, and perform user attribution.

| Case ID | Malware Family | Key Outcomes & Observations |
| :--- | :--- | :--- |
| **Case 1** | [NetSupport RAT](./pcap-analysis/case-1-netsupport-rat/report.md) | Identified encrypted command-and-control beaconing over TCP 443; performed user and host attribution via NBNS and Kerberos traffic. |
| **Case 2** | [TrickBot](./pcap-analysis/case-2-trickbot/report.md) | Reconstructed a drive-by download infection chain; extracted malicious binary objects from HTTP traffic; identified transition to encrypted TLS C2 channels. |
| **Case 3** | [Lumma Stealer](./pcap-analysis/case-3-lumma-fingerprinting/report.md) | Detected endpoint fingerprinting activity via malicious JavaScript payloads designed to collect system, browser, and hardware telemetry. |

---

## 🔬 Investigation Methodology

Each case in this repository strictly adheres to a standard SOC workflow to ensure accurate, repeatable, and thorough investigations:

1.  **Telemetry Collection:** Ingesting raw logs (Sysmon, Firewall) or capturing PCAP data.
2.  **Parsing & Extraction:** Utilizing tools like Splunk SPL (`rex`) or Wireshark HTTP object extraction to isolate relevant data fields.
3.  **Indicator Pivoting:** Expanding the search scope using identified IPs, ports, and domains.
4.  **Behavioral Analysis:** Evaluating frequency, timing, and volume to identify automated or malicious patterns.
5.  **Attribution:** Linking malicious activity to specific internal hosts and user accounts.
6.  **Reporting:** Documenting evidence, assessing risk severity, and providing actionable remediation steps.

---

## 🛠️ Tools & Technologies

* **Analysis:** Splunk Enterprise, Wireshark, VirusTotal
* **Telemetry:** Windows Firewall Logs, Sysmon, Windows Event Logs
* **Offensive Simulation:** Kali Linux, PowerShell

---

## 👤 Author

**Sai Shashank P**
*SOC Analyst*
Dedicated to Threat Detection, Incident Response, and Security Engineering.
