# Security Incident Report

**Case ID:** SOC-TRAFFIC-003
**Incident Type:** Malware Activity (Lumma Stealer – Fingerprinting)
**Date of Analysis:** 2026-04-10
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

On 2026-01-27 at approximately 23:05 UTC, suspicious network activity was identified involving communication between an internal Windows host and a malicious IP address (153.92.1.49).

The affected system accessed the malicious domain whitepepper.su, which delivered a JavaScript-based fingerprinting payload associated with Lumma Stealer. The script collected system, browser, and hardware information.

No confirmed data exfiltration or persistent command-and-control communication was observed in the captured traffic.

---

## 2. Scope of Investigation

* Data Source: PCAP
* Network Range: 10.1.28.0/24
* Domain: win11office.com

---

## 3. Indicators of Compromise (IoCs)

| Type             | Value          |
| ---------------- | -------------- |
| Malicious IP     | 153.92.1.49    |
| Malicious Domain | whitepepper.su |
| Protocol         | HTTP           |
| Malware          | Lumma Stealer  |

---

## 4. Affected Asset Details

| Attribute   | Value             |
| ----------- | ----------------- |
| IP Address  | 10.1.28.58        |
| MAC Address | 00:21:5d:c8:0e:f2 |
| Hostname    | DESKTOP-ES9F3ML   |

---

## 5. User Attribution

| Attribute | Value         |
| --------- | ------------- |
| Username  | gwyatt        |
| Domain    | WIN11OFFICE   |
| Full Name | Gabriel Wyatt |

---

## 6. Investigation & Analysis

### 6.1 Baseline Activity

The host generated normal traffic prior to the incident, including Microsoft connectivity checks and requests to Google services.

![Baseline](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/01-baseline-connectivity.png)

---

### 6.2 Malicious Domain Contact

The host initiated an HTTP request to the malicious domain:

```
whitepepper.su/api/set_agent
```

![Malicious Request](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/02-malicious-domain-request.png)

---

### 6.3 Fingerprinting Payload

The HTTP response contained a JavaScript payload designed to collect system, browser, and hardware information.

![Fingerprint Script](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/03-fingerprinting-script.png)

---

### 6.4 Fingerprinting Behavior

Repeated requests to the endpoint `/api/set_agent` were observed, indicating active fingerprinting activity.

Although the script includes functionality for data exfiltration via HTTP POST, no such requests were observed in the PCAP.

![Fingerprint Behavior](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/04-fingerprinting-behavior.png)

---

### 6.5 Connection Termination

The session was terminated by the client, with no further communication observed.

```
10.1.28.58 → 153.92.1.49 [RST, ACK]
```

![Termination](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/05-connection-termination.png)

---

### 6.6 Host and User Identification

Hostname identified via NBNS:

```
DESKTOP-ES9F3ML
```

![Hostname](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/06-hostname-nbns.png)

---

Username identified via Kerberos:

```
gwyatt
```

![Username](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/07-username-kerberos.png)

---

Full name identified via DCERPC:

```
Gabriel Wyatt
```

![Full Name](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/08-fullname-dcerpc.png)

---

MAC address identified from Ethernet frame:

```
00:21:5d:c8:0e:f2
```

![MAC](https://raw.githubusercontent.com/Sai-shashank-2005/soc-traffic-analysis/main/case-3-lumma-fingerprinting/screenshots/09-mac-address.png)

---

## 7. Findings

* The host 10.1.28.58 (DESKTOP-ES9F3ML) communicated with malicious infrastructure
* The domain whitepepper.su delivered a fingerprinting payload
* Activity is consistent with Lumma Stealer reconnaissance behavior
* No confirmed data exfiltration was observed
* No persistent command-and-control activity was identified

---

## 8. Risk Assessment

| Category   | Assessment                      |
| ---------- | ------------------------------- |
| Severity   | Medium                          |
| Impact     | System profiling                |
| Likelihood | Confirmed malicious interaction |

---

## 9. Recommendations

* Isolate the affected host
* Block malicious IP and domain
* Perform endpoint security scan
* Monitor for recurring activity
* Implement detection rules for suspicious HTTP behavior

---

## 10. Conclusion

The investigation confirms that the host DESKTOP-ES9F3ML was targeted by Lumma Stealer infrastructure and subjected to browser fingerprinting. The activity was limited to reconnaissance, with no evidence of further exploitation within the captured traffic.

---
