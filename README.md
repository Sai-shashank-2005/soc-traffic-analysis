# SOC Traffic Analysis Lab

## Overview

This repository documents hands-on Security Operations Center (SOC) investigations performed using both **SIEM (Splunk)** and **network traffic analysis (Wireshark)**.

The lab simulates real-world detection and incident response workflows, focusing on identifying malicious activity, validating threats, and producing professional, evidence-based security reports.

---

## Core Focus Areas

* SIEM-based threat detection (Splunk)
* Network traffic analysis (PCAP investigations)
* Attack simulation and detection engineering
* Log analysis (Windows, Sysmon, Firewall)
* Incident response and reporting

---

## Key Capabilities

* Detection of reconnaissance activities (port scanning, enumeration)
* Identification of malware behavior through network traffic
* Correlation of logs across multiple data sources
* Reconstruction of attack chains from initial access to impact
* Differentiation between benign and malicious activity
* Development of structured SOC incident reports

---

## Case Categories

### 🔹 SIEM Detection (Splunk)

| Case   | Title                              | Description                                                          |
| ------ | ---------------------------------- | -------------------------------------------------------------------- |
| Case 1 | Port Scan Detection                | Detected reconnaissance activity using firewall logs and SPL queries |
| Case 2 | Brute Force Detection *(Upcoming)* | Detect authentication attacks using Windows/Sysmon logs              |

---

### 🔹 Network Traffic Analysis (Wireshark)

| Case   | Malware        | Key Outcome                                              |
| ------ | -------------- | -------------------------------------------------------- |
| Case 3 | NetSupport RAT | Identified remote access activity and beaconing behavior |
| Case 4 | TrickBot       | Reconstructed infection chain and C2 communication       |
| Case 5 | Lumma Stealer  | Detected victim fingerprinting and attribution           |

---

## Investigation Methodology

Each case follows a structured SOC workflow:

1. Alert or anomaly detection
2. Data collection and log analysis
3. Field extraction and parsing
4. Indicator pivoting (IP, ports, domains)
5. Behavioral analysis
6. Attack pattern identification
7. Evidence correlation
8. Reporting and recommendations

---

## Repository Structure

```
soc-traffic-analysis/
├── splunk/
│   └── case-1-port-scan-detection/
│       ├── screenshots/
│       └── report.md
│
├── wireshark/
│   ├── case-1-netsupport-rat/
│   ├── case-2-trickbot/
│   └── case-3-lumma-fingerprinting/
```

---

## Tools & Technologies

* Splunk (SIEM)
* Wireshark (Packet Analysis)
* Windows Firewall Logs
* Sysmon (Endpoint Telemetry)
* Kali Linux (Attack Simulation)
* Threat Intelligence (VirusTotal)

---

## Key Insights

* Behavioral detection is more reliable than signature-based detection
* Reconnaissance activity (port scanning) is an early indicator of attacks
* Log correlation across sources significantly improves detection accuracy
* Proper field extraction is critical for effective SIEM analysis

---

## Professional Value

This lab demonstrates:

* Practical SOC analyst skills
* Real-world detection engineering
* Log analysis and threat identification
* Structured incident reporting
* Hands-on SIEM experience

---

## Author

**Sai Shashank P**
SOC Analyst
Focused on Threat Detection, Incident Response, and Security Engineering
