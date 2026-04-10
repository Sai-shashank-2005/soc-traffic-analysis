# 🛡️ Security Incident Report

**Case ID:** SOC-TRAFFIC-003
**Incident Type:** Malware Activity (Lumma Stealer – Fingerprinting)
**Date of Analysis:** 2026-04-10
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

On 2026-01-27 at approximately 23:05 UTC, suspicious network activity was identified involving communication between an internal Windows host and a known malicious IP address (153.92.1.49).

The affected system accessed a malicious domain (**whitepepper.su**), which delivered a JavaScript-based fingerprinting payload associated with Lumma Stealer activity. The script collected system, browser, and hardware information from the victim.

No sustained command-and-control (C2) communication or confirmed data exfiltration was observed in the captured traffic. The activity is classified as reconnaissance and victim profiling.

---

## 2. Scope of Investigation

* **Data Source:** Network packet capture (PCAP)
* **Network Range:** 10.1.28.0/24
* **Domain Environment:** win11office.com

---

## 3. Indicators of Compromise (IoCs)

| Type             | Value          |
| ---------------- | -------------- |
| Malicious IP     | 153.92.1.49    |
| Malicious Domain | whitepepper.su |
| Protocol         | HTTP           |
| Port             | 80             |
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

---

### 6.1 Baseline Activity (Benign Traffic)

Filter used:

```
http.request
```

* Observed legitimate connectivity checks:

```
GET /connecttest.txt
```

* Additional normal traffic:

```
GET /time/1/current
```

👉 Confirms **normal system behavior prior to incident**

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/01-baseline-connectivity.png)

---

### 6.2 Initial Malicious Contact

Filter used:

```
ip.addr == 153.92.1.49 && http
```

* Identified request to malicious domain:

```
http://whitepepper.su/api/set_agent
```

👉 Marks **initial attacker interaction**

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/02-malicious-domain-request.png)

---

### 6.3 Fingerprinting Payload Delivery

* HTTP response contained embedded JavaScript performing system fingerprinting

* Script collected:

  * System & OS details
  * Browser & user-agent info
  * Hardware characteristics
  * Canvas & WebGL fingerprint
  * Network information

👉 Confirms **victim profiling and reconnaissance**

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/03-fingerprinting-script.png)

---

### 6.4 Fingerprinting Behavior

* Observed repeated interaction with attacker endpoint:

```
/api/set_agent
```

👉 Indicates **active fingerprinting activity**

* Although script contains POST functionality, **no POST request observed in PCAP**

👉 No confirmed data exfiltration within captured traffic

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/04-fingerprinting-behavior.png)

---

### 6.5 Connection Termination

* Final observed packet:

```
10.1.28.58 → 153.92.1.49  [RST, ACK]
```

👉 Indicates **session termination**

* No further communication observed
* No persistent C2 activity detected

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/05-connection-termination.png)

---

### 6.6 Host & User Identification

* Hostname identified via NBNS:

```
DESKTOP-ES9F3ML
```

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/06-hostname-nbns.png)

---

* Username identified via Kerberos:

```
gwyatt
```

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/07-username-kerberos.png)

---

* Full name identified via DCERPC:

```
Gabriel Wyatt
```

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/08-fullname-dcerpc.png)

---

* MAC Address identified via Ethernet II:

```
00:21:5d:c8:0e:f2
```

🔗 [View Screenshot](https://github.com/Sai-shashank-2005/soc-portfolio/blob/main/case-3-lumma-fingerprinting/screenshots/09-mac-address.png)

---

## 7. Findings

* Host **10.1.28.58 (DESKTOP-ES9F3ML)** communicated with malicious infrastructure
* Malicious domain **whitepepper.su** delivered fingerprinting payload
* Activity consistent with **Lumma Stealer reconnaissance stage**
* System and browser fingerprinting successfully executed
* No confirmed data exfiltration or persistent C2 observed
* Activity limited to **initial reconnaissance phase**

---

## 8. Risk Assessment

| Category   | Assessment                                   |
| ---------- | -------------------------------------------- |
| Severity   | Medium                                       |
| Impact     | System profiling, potential future targeting |
| Likelihood | Confirmed malicious interaction              |

---

## 9. Recommendations

* Isolate affected host for further inspection
* Block malicious indicators:

  * 153.92.1.49
  * whitepepper.su
* Perform endpoint malware scan
* Monitor for repeated connections to attacker infrastructure
* Implement detection rules for:

  * Suspicious HTTP API calls
  * Browser fingerprinting behavior

---

## 10. Conclusion

The investigation confirms that the system DESKTOP-ES9F3ML was targeted by Lumma Stealer infrastructure and subjected to browser-based fingerprinting. The activity was limited to reconnaissance and profiling, with no confirmed follow-up exploitation within the captured traffic. Preventive monitoring and defensive controls are recommended to mitigate further risk.

---
