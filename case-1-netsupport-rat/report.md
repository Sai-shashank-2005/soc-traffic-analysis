# 🛡️ Security Incident Report

**Case ID:** SOC-TRAFFIC-001
**Incident Type:** Malware Infection (NetSupport Manager RAT)
**Date of Analysis:** 2026-02-28
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

A SIEM alert identified suspicious outbound traffic associated with **NetSupport Manager RAT** communicating with a known malicious IP address (**45.131.214.85**) over TCP port 443.

PCAP analysis confirmed that an internal host was compromised and engaged in repeated encrypted outbound communication consistent with command-and-control (C2) activity. The affected system and associated user account were identified.

---

## 2. Scope of Investigation

* **Data Source:** Network packet capture (PCAP)
* **Network Range:** 10.2.28.0/24
* **Domain Environment:** EASYAS123

---

## 3. Indicators of Compromise (IoCs)

| Type         | Value          |
| ------------ | -------------- |
| Malicious IP | 45.131.214.85  |
| Protocol     | TCP            |
| Port         | 443 (HTTPS)    |
| Threat       | NetSupport RAT |

---

## 4. Affected Asset Details

| Attribute   | Value             |
| ----------- | ----------------- |
| IP Address  | 10.2.28.88        |
| MAC Address | 00:19:d1:b2:4d:ad |
| Hostname    | DESKTOP-TEYQ2NR   |

---

## 5. User Attribution

| Attribute | Value                        |
| --------- | ---------------------------- |
| Username  | brolf                        |
| Domain    | EASYAS123                    |
| Full Name | Not observed in PCAP traffic |

---

## 6. Investigation & Analysis

### 6.1 IoC-Based Traffic Pivot

Filter used:

```
ip.addr == 45.131.214.85
```

Evidence:
[IoC Pivot](https://github.com/Sai-shashank-2005/soc-traffic-analysis/blob/main/case-1-netsupport-rat/screenshots/ioc-pivot.png)

* Identified internal host communicating with malicious IP
* Confirmed infected system: **10.2.28.88**

---

### 6.2 Directional Traffic Analysis

Filter used:

```
ip.src == 10.2.28.88 and ip.dst == 45.131.214.85
```

* Confirmed outbound communication initiated from infected host
* Established clear attacker-victim relationship

---

### 6.3 Network Behavior Analysis (C2 Activity)

Evidence:
[C2 Traffic](https://github.com/Sai-shashank-2005/soc-traffic-analysis/blob/main/case-1-netsupport-rat/screenshots/c2-traffic.png)

* Repeated outbound connections observed:

  ```
  10.2.28.88 → 45.131.214.85:443
  ```
* Repeated HTTPS traffic suggests **beaconing behavior**
* Activity consistent with RAT-based command-and-control communication

---

### 6.4 Host Identification (NBNS Analysis)

Filter used:

```
nbns
```

Evidence:
[Hostname Identification](https://github.com/Sai-shashank-2005/soc-traffic-analysis/blob/main/case-1-netsupport-rat/screenshots/hostname-nbns.png)

* Hostname extracted from NBNS registration traffic

---

### 6.5 User Identification (Kerberos Analysis)

Filter used:

```
kerberos.CNameString
```

Evidence:
[Username Extraction](https://github.com/Sai-shashank-2005/soc-traffic-analysis/blob/main/case-1-netsupport-rat/screenshots/username-kerberos.png)

* Username identified from Kerberos authentication traffic

---

## 7. Findings

* Host **10.2.28.88 (DESKTOP-TEYQ2NR)** is confirmed compromised
* System communicates with known malicious infrastructure
* Communication occurs over encrypted channel (TCP 443)
* Repeated outbound HTTPS connections indicate **beaconing behavior**
* Behavior aligns with **NetSupport RAT command-and-control activity**
* User account **brolf** associated with infected system

---

## 8. Risk Assessment

| Category   | Assessment                                     |
| ---------- | ---------------------------------------------- |
| Severity   | High                                           |
| Impact     | System compromise, potential data exfiltration |
| Likelihood | Confirmed active infection                     |

---

## 9. Recommendations

* Isolate affected host immediately
* Block malicious IP (45.131.214.85) at network perimeter
* Reset credentials for affected user account
* Perform endpoint malware removal
* Conduct further investigation for lateral movement

---

## 10. Conclusion

The investigation confirms that the system **DESKTOP-TEYQ2NR** is infected with NetSupport RAT and actively communicating with an external attacker-controlled server. Immediate containment and remediation actions are required to prevent further compromise.

---
