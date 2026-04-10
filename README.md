# 🛡️ SOC Traffic Analysis Lab

## Overview

This repository showcases end-to-end network traffic investigations performed in a SOC-style workflow. Each case study demonstrates the ability to analyze packet captures (PCAP), identify malicious activity, reconstruct attack chains, and produce professional incident reports aligned with real-world SOC operations.

---

## Objectives

* Perform structured traffic analysis using Wireshark
* Identify malware delivery mechanisms and infection points
* Detect command-and-control (C2) communications
* Differentiate normal vs malicious network behavior
* Reconstruct full attack timelines
* Document findings in a professional incident report format

---

## Core Competencies Demonstrated

* Network protocol analysis (DNS, HTTP, TLS, TCP)
* Threat hunting and investigative pivoting
* Malware delivery and execution analysis
* Behavioral detection (beyond static IoCs)
* Incident triage and validation
* SOC reporting and communication

---

## Repository Structure

```
soc-traffic-analysis/
├── case-1-netsupport-rat/
│   ├── screenshots/
│   └── report.md
├── case-2-dynaccountic/
│   ├── screenshots/
│   └── report.md
```

---

## Case Studies

### Case 1: NetSupport RAT Infection

* Identified compromised host via IoC-based pivoting
* Confirmed outbound encrypted communication to known malicious infrastructure
* Observed repeated HTTPS traffic consistent with beaconing behavior
* Extracted host and user attribution from network telemetry

---

### Case 2: TrickBot Malware Infection (Dynaccountic)

* Identified initial infection via HTTP binary download (`ser0410.bin`)
* Validated malware using external threat intelligence (VirusTotal)
* Reconstructed attack chain: DNS → Payload Delivery → Execution → C2
* Detected encrypted communication over non-standard port (449)
* Distinguished delivery infrastructure from command-and-control behavior

---

## SOC Workflow Applied

1. Alert / anomaly identification
2. Data scoping and traffic filtering
3. Indicator pivoting (IP, domain, file)
4. Behavioral analysis and pattern recognition
5. Attack chain reconstruction
6. Asset identification and impact assessment
7. Containment and remediation recommendations

---

## Tools & Environment

* Wireshark (packet analysis)
* VirusTotal (malware verification)
* GitHub (documentation and case reporting)

---

## Key Insights

* Effective detection relies on behavior, not just indicators
* Malware frequently uses encrypted channels (TLS) to evade inspection
* Timeline correlation is critical for understanding attack progression
* Not all traffic is suspicious — accurate filtering is essential in SOC environments

---

## Professional Focus

This repository is designed to reflect practical SOC analyst capabilities, including:

* Real-world investigation methodology
* Clear and defensible reasoning
* Evidence-backed conclusions
* Actionable security recommendations

---

## Author

Sai Shashank P
Aspiring SOC Analyst | Focused on Threat Detection, Incident Response, and Network Security Analysis
