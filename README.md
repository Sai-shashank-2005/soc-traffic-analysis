# SOC Traffic Analysis Lab

## Overview

This repository documents multiple real-world network traffic investigations conducted using a SOC-style workflow. Each case simulates analyst-driven incident response, focusing on identifying malicious activity, reconstructing attack chains, and producing evidence-backed security reports.

The work reflects practical experience in analyzing PCAP data, validating threats, and performing attribution of compromised systems and users.

---

## Key Capabilities

* Detection of malware activity through network traffic analysis
* Reconstruction of attack chains from initial access to command-and-control
* Identification of infected hosts and user attribution
* Differentiation between benign and malicious network behavior
* Analysis of real-world malware families (NetSupport RAT, TrickBot, Lumma Stealer)
* Development of structured, evidence-based incident reports

---

## Case Highlights

| Case   | Malware        | Key Outcome                                                                    |
| ------ | -------------- | ------------------------------------------------------------------------------ |
| Case 1 | NetSupport RAT | Identified remote access activity and beaconing behavior                       |
| Case 2 | TrickBot       | Reconstructed full infection chain and C2 communication over non-standard port |
| Case 3 | Lumma Stealer  | Detected victim fingerprinting and performed full host/user attribution        |

---

## Investigation Approach

Each case follows a consistent SOC investigation methodology:

1. Alert or anomaly identification
2. Traffic scoping and filtering
3. Indicator pivoting (IP, domain, file artifacts)
4. Behavioral analysis and pattern recognition
5. Attack chain reconstruction
6. Asset and user attribution
7. Impact assessment and response recommendations

---

## Repository Structure

```
soc-traffic-analysis/
├── case-1-netsupport-rat/
├── case-2-trickbot/
├── case-3-lumma-fingerprinting/
│   ├── screenshots/
│   └── report.md
```

Each case contains:

* A detailed incident report
* Supporting packet-level evidence (screenshots)
* Documented analysis aligned with SOC workflows

---

## Tools & Techniques

* Wireshark for packet-level analysis
* Threat intelligence validation (VirusTotal)
* Protocol analysis (DNS, HTTP, TLS, TCP)
* Behavioral detection and traffic pattern analysis

---

## Key Observations

* Malware frequently leverages legitimate protocols (HTTP/TLS) to evade detection
* Behavioral analysis is more reliable than static indicators alone
* Accurate timeline reconstruction is critical for understanding attack progression
* Effective filtering is essential to separate benign traffic from malicious activity

---

## Professional Context

This work demonstrates practical SOC analyst capabilities, including:

* Structured investigation methodology
* Evidence-based reasoning and validation
* Clear and concise incident reporting
* Focus on real-world detection and analysis scenarios

---

## Author

Sai Shashank P
SOC Analyst 
Focused on Threat Detection, Incident Response, and Network Traffic Analysis

---
