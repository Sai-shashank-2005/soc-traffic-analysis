# 🛡️ Security Incident Report

**Case ID:** SOC-TRAFFIC-001
**Incident Type:** Malware Infection (NetSupport Manager RAT)
**Analysis Date:** 2026-02-28
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

A SIEM alert identified suspicious outbound traffic associated with **NetSupport Manager RAT** communicating with a known malicious IP (**45.131.214.85**) over TCP port 443.

Packet capture analysis confirmed that an internal host was compromised and engaged in repeated encrypted communication consistent with command-and-control (C2) activity. The affected system and associated user account were identified.

---

## 2. Scope

* **Data Source:** PCAP (network traffic capture)
* **Network Range:** 10.2.28.0/24
* **Domain:** EASYAS123

---

## 3. Indicators of Compromise (IoCs)

| Type         | Value          |
| ------------ | -------------- |
| Malicious IP | 45.131.214.85  |
| Protocol     | TCP            |
| Port         | 443 (HTTPS)    |
| Threat       | NetSupport RAT |

---

## 4. Affected Asset

| Attribute   | Value             |
| ----------- | ----------------- |
| IP Address  | 10.2.28.88        |
| MAC Address | 00:19:d1:b2:4d:ad |
| Hostname    | DESKTOP-TEYQ2NR   |

---

## 5. User Attribution

| Attribute | Value                |
| --------- | -------------------- |
| Username  | brolf                |
| Domain    | EASYAS123            |
| Full Name | Not observed in PCAP |

---

## 6. Investigation Details

### 6.1 IoC Pivot (Initial Detection)

Filter used:

```
ip.addr == 45.131.214.85
```

Evidence:
[IoC Pivot Screenshot](./case-1-netsupport-rat/screenshots/ioc-pivot.png)

* Identified internal host communicating with malicious IP
* Source host confirmed: **10.2.28.88**

---

### 6.2 Network Behavior Analysis (C2 Communication)

Evidence:
[C2 Traffic Screenshot](./case-1-netsupport-rat/screenshots/c2-traffic.png)

* Repeated outbound connections observed:

  ```
  10.2.28.88 → 45.131.214.85:443
  ```
* Behavior consistent with persistent encrypted command-and-control (C2)

---

### 6.3 Host Identification (NBNS Analysis)

Filter used:

```
nbns
```

Evidence:
[Hostname Identification](./case-1-netsupport-rat/screenshots/hostname-nbns.png)

* Hostname extracted from NBNS registration traffic

---

### 6.4 User Identification (Kerberos Analysis)

Filter used:

```
kerberos.CNameString
```

Evidence:
[Username Extraction](./case-1-netsupport-rat/screenshots/username-kerberos.png)

* Username identified from Kerberos authentication traffic

---

## 7. Findings

* Host **10.2.28.88 (DESKTOP-TEYQ2NR)** is confirmed compromised
* System communicates with known malicious infrastructure
* Communication occurs over encrypted channel (TCP 443)
* Pattern indicates active command-and-control (C2) behavior
* User account **brolf** associated with infected system

---

## 8. Risk Assessment

| Category | Assessment                                     |
| -------- | ---------------------------------------------- |
| Severity | High                                           |
| Impact   | System compromise, potential data exfiltration |
| Status   | Active threat detected                         |

---

## 9. Recommendations

* Isolate infected host immediately
* Block malicious IP (45.131.214.85) at network perimeter
* Reset credentials for affected user account
* Perform endpoint malware removal
* Conduct further investigation for lateral movement

---

## 10. Conclusion

Analysis confirms that the system **DESKTOP-TEYQ2NR** is infected with NetSupport RAT and actively communicating with an external attacker-controlled server. Immediate containment and remediation actions are required to prevent further compromise.

---
