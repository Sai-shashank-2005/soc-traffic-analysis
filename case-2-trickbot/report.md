# 🛡️ Security Incident Report

**Case ID:** SOC-TRAFFIC-002
**Incident Type:** Malware Infection (TrickBot)
**Date of Analysis:** 2026-04-09
**Analyst:** Sai Shashank P

---

## 1. Executive Summary

On 2018-04-11 at approximately 10:04:09 UTC, a Windows computer used by the machine account BATISTE-PC$ was infected with TrickBot malware. This infection probably originated from a drive-by download involving the domain caveaudelteatro.it, which delivered a malicious binary file (ser0410.bin). The infected computer was isolated from the network, malicious IP addresses were blocked, and remediation actions including malware removal and credential resets were initiated.

---

## 2. Scope of Investigation

* **Data Source:** Network packet capture (PCAP)
* **Network Range:** 10.10.10.0/24
* **Domain Environment:** dynaccountic.com

---

## 3. Indicators of Compromise (IoCs)

| Type             | Value              |
| ---------------- | ------------------ |
| Malicious Domain | caveaudelteatro.it |
| Delivery IP      | 95.110.193.132     |
| C2 IP            | 82.214.141.134     |
| Protocol         | HTTP, TLS          |
| Ports            | 80, 449            |
| Malware          | TrickBot           |

---

## 4. Affected Asset Details

| Attribute   | Value             |
| ----------- | ----------------- |
| IP Address  | 10.10.10.209      |
| MAC Address | 00:30:67:f1:2d:63 |
| Hostname    | BATISTE-PC        |

---

## 5. User Attribution

| Attribute | Value                                 |
| --------- | ------------------------------------- |
| Username  | Not observed in PCAP                  |
| Domain    | dynaccountic.com                      |
| Notes     | Machine account observed: BATISTE-PC$ |

---

## 6. Investigation & Analysis

---

### 6.1 Payload Delivery (Initial Infection)

Filter used:

```
http.request
```

* Identified malicious HTTP request:

```
GET /ser0410.bin
```

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/payload-download.png)

![Payload Download](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/payload-download.png)

* Source: 10.10.10.209
* Destination: 95.110.193.132
* Host: caveaudelteatro.it

👉 Confirms **initial malware delivery**

---

### 6.2 Malware Extraction (HTTP Objects)

* Extracted file from HTTP traffic:

```
ser0410.bin (~364 KB)
```

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/http-object.png)

![HTTP Object](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/http-object.png)

👉 Confirms **binary payload transfer**

---

### 6.3 Malware Verification (VirusTotal)

* File analyzed in VirusTotal
* Detected as **TrickBot malware**

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/virustotal.png)

![VirusTotal](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/virustotal.png)

👉 Confirms **malicious nature of payload**

---

### 6.4 DNS Resolution Analysis

Filter used:

```
dns
```

* Domain resolved:

```
caveaudelteatro.it → 95.110.193.132
```

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/dns-resolution.png)

![DNS Resolution](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/dns-resolution.png)

👉 Links **domain to delivery infrastructure**

---

### 6.5 Command-and-Control (C2) Communication

Filter used:

```
ip.addr == 82.214.141.134
```

* Observed repeated encrypted communication:

```
10.10.10.209 → 82.214.141.134:449
```

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/c2-traffic.png)

![C2 Traffic](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/c2-traffic.png)

* TLS handshake + encrypted data observed
* Repeated connections over time

👉 Indicates **C2 beaconing behavior**

---

### 6.6 Host Identification

Filter used:

```
nbns
```

[View Screenshot](https://github.com/<your-repo>/case-2-dynaccountic/screenshots/hostname.png)

![Hostname](https://raw.githubusercontent.com/<your-repo>/case-2-dynaccountic/screenshots/hostname.png)

* Hostname identified as:

```
BATISTE-PC
```

---

## 7. Findings

* Host **10.10.10.209 (BATISTE-PC)** is confirmed compromised
* Malware delivered via HTTP from **caveaudelteatro.it**
* Payload identified as **TrickBot banking trojan**
* Infection likely occurred via **drive-by download**
* Post-infection behavior shows transition to encrypted TLS communication
* Repeated communication with **82.214.141.134:449** indicates C2 activity
* Additional outbound connections suggest possible scanning/propagation

---

## 8. Risk Assessment

| Category   | Assessment                                    |
| ---------- | --------------------------------------------- |
| Severity   | High                                          |
| Impact     | System compromise, potential credential theft |
| Likelihood | Confirmed active infection                    |

---

## 9. Recommendations

* Isolate affected host immediately
* Block malicious IPs:

  * 95.110.193.132
  * 82.214.141.134
* Perform endpoint malware removal
* Reset credentials associated with the host
* Monitor for additional infected systems
* Deploy detection rules for:

  * Binary downloads followed by TLS on non-standard ports

---

## 10. Conclusion

The investigation confirms that the system BATISTE-PC was infected with TrickBot malware via a malicious binary download. Post-infection activity shows encrypted communication with external infrastructure over a non-standard port, consistent with command-and-control behavior. Immediate containment and remediation actions are required.

---
