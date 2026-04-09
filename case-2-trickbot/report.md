# 🛡️ Security Incident Report

**Case ID:** SOC-TRAFFIC-002
**Incident Type:** Malware Infection (Trickbot)
**Date of Analysis:** 2026-04-09
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

A network traffic investigation identified a malware infection on an internal Windows host following the download of a malicious binary from an external domain. Analysis confirmed that the payload was a **Trickbot banking trojan**, delivered over HTTP as a disguised binary file.

Post-infection activity included external IP reconnaissance and encrypted outbound communication to suspicious infrastructure over non-standard ports, consistent with command-and-control (C2) behavior.

---

## 2. Scope of Investigation

* **Data Source:** Network Packet Capture (PCAP)
* **Network Range:** 10.10.10.0/24
* **Domain Environment:** dynaccountic.com

---

## 3. Indicators of Compromise (IoCs)

| Type             | Value              |
| ---------------- | ------------------ |
| Malicious Domain | caveaudelteatro.it |
| Malicious IP     | 95.110.193.132     |
| C2 IP            | 82.214.141.134     |
| C2 IP            | 86.61.160.50       |
| Protocols        | HTTP, TLS          |
| Ports            | 80, 447, 449       |
| Malware          | Trickbot           |

---

## 4. Affected Asset Details

| Attribute   | Value             |
| ----------- | ----------------- |
| IP Address  | 10.10.10.209      |
| MAC Address | 00:30:67:f1:2d:63 |
| Hostname    | BATISTE-PC        |

---

## 5. User Attribution

| Attribute | Value            |
| --------- | ---------------- |
| Username  | winford.batiste  |
| Domain    | dynaccountic.com |
| Source    | Kerberos Traffic |

---

## 6. Investigation & Analysis

### 6.1 IoC-Based Traffic Pivot

Filter used:

```
ip.addr == 95.110.193.132
```

![IoC Pivot](./screenshots/01-infection-vector.png)

* Identified internal host communicating with external malicious infrastructure
* Confirmed infected system: **10.10.10.209**

---

### 6.2 Payload Delivery Analysis

Filter used:

```
http.request
```

![Payload Download](./screenshots/02-payload-download.png)

* Suspicious HTTP request observed:

```
GET /ser0410.bin HTTP/1.1
Host: caveaudelteatro.it
```

* Server response:

  * `HTTP/1.1 200 OK`
  * File size: **364,544 bytes**
  * Content-Type: application/octet-stream

* Traffic pattern:

  * Large server-to-client packets (~1460 bytes)
  * Continuous transfer indicates file download

---

### 6.3 Malware Validation

![MZ Header](./screenshots/03-mz-header.png)

* Extracted file (`ser0410.bin`) analysis:

  * Presence of **MZ header (4D 5A)**
  * Confirms Windows PE executable

* Hash analysis:

  * SHA256: `c2c1e2c22f67dda6553cbcc173694b68677b77319243684925e8dc3f78b3dbf8`
  * Matches known **Trickbot malware**

---

### 6.4 Post-Infection Behavior

Filter used:

```
http.request
```

![IP Recon](./screenshots/04-ip-recon.png)

* Observed request:

```
GET /raw HTTP/1.1
Host: myexternalip.com
```

* Indicates external IP lookup performed by malware
* Common reconnaissance behavior post-infection

---

### 6.5 Command-and-Control (C2) Activity

Filter used:

```
ip.addr == 10.10.10.209 && (tcp.port == 447 || tcp.port == 449)
```

![C2 Traffic](./screenshots/05-c2-traffic.png)

* Encrypted outbound communication observed:

```
10.10.10.209 → 82.214.141.134:449
10.10.10.209 → 86.61.160.50:447
```

* Characteristics:

  * TLS encrypted traffic
  * Non-standard ports
  * Repeated outbound connections

* Behavior consistent with **Trickbot C2 communication**

---

### 6.6 Host Identification (NBNS Analysis)

Filter used:

```
nbns
```

![Hostname](./screenshots/06-hostname.png)

* Hostname identified: **BATISTE-PC**

---

### 6.7 User Identification (Kerberos Analysis)

Filter used:

```
kerberos.CNameString and !(kerberos.CNameString contains "$")
```

![Username](./screenshots/07-username.png)

* User identified: **winford.batiste**

---

## 7. Findings

* Host **10.10.10.209 (BATISTE-PC)** is confirmed compromised
* Malware identified as **Trickbot banking trojan**
* Infection initiated via malicious HTTP download
* Payload delivered as disguised executable (`.bin`)
* Post-infection reconnaissance observed
* Encrypted outbound communication confirms active C2
* User **winford.batiste** associated with infected system

---

## 8. Risk Assessment

| Category   | Assessment                                          |
| ---------- | --------------------------------------------------- |
| Severity   | Critical                                            |
| Impact     | Credential theft, financial fraud, lateral movement |
| Likelihood | Confirmed active compromise                         |

---

## 9. Recommendations

* Isolate affected host immediately
* Block malicious IPs and domains at network perimeter
* Reset credentials for affected user
* Perform full endpoint remediation
* Monitor for lateral movement and persistence mechanisms
* Deploy SIEM detection rules for similar activity

---

## 10. Conclusion

The investigation confirms that the system **BATISTE-PC** was infected with Trickbot malware following a malicious payload download from an external domain. The host exhibited post-infection reconnaissance and active encrypted communication with attacker-controlled infrastructure, indicating an ongoing compromise requiring immediate containment and remediation.

---
