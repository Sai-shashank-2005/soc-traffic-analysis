# Splunk SIEM Lab

## Overview

This section of the repository focuses on **SIEM-based threat detection using Splunk**.
The lab simulates real-world SOC workflows by ingesting endpoint and network logs, developing detection queries, and validating suspicious activity through structured analysis.

---
## Architecture

![SOC Lab Architecture Diagram](assests/architecture.png)


## Scope

The Splunk lab covers:

* Log ingestion from Windows systems (Sysmon, Event Logs, Firewall)
* Detection engineering using Splunk Processing Language (SPL)
* Identification of suspicious behaviors (reconnaissance, execution, authentication events)
* Correlation of network and endpoint activity
* Development of SOC-style detection use cases

---

## Detection Focus

The cases in this section emphasize high-value detection scenarios:

* Reconnaissance activity (port scanning)
* Suspicious process execution (PowerShell, command-line abuse)
* Authentication anomalies (brute force attempts)
* Network connections and potential C2 behavior

---

## Approach

Each case follows a structured detection workflow:

1. Log collection and ingestion
2. Field extraction and normalization
3. Detection query development
4. Behavioral analysis
5. Evidence validation
6. Documentation of findings

---

## Structure

```text id="vxt2hm"
splunk/
├── case-1-port-scan-detection/
├── case-2-...
```

Each case includes:

* Detection queries (SPL)
* Supporting evidence (screenshots)
* SOC-style incident report

---

## Objective

The goal of this lab is to demonstrate practical experience in:

* SIEM operations and log analysis
* Detection engineering
* Threat identification and validation
* Professional SOC reporting

---
