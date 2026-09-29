# Black-Box Web Server Penetration Testing Assessment

**Author:** Izaan Shumaiz  
**Role:** Cybersecurity Analyst / Penetration Tester  
**Testing Methodology:** Black-Box Penetration Testing  
**Primary Tools:** Kali Linux, Nmap, Nessus, Gobuster, Nikto, WhatWeb, Hydra, Metasploit Framework  

---

## Executive Summary

This repository documents an end-to-end black-box penetration testing assessment and vulnerability analysis conducted against a target web server infrastructure[cite: 8]. The assessment simulated a real-world external attack scenario, moving through full operational stages: initial reconnaissance, port and service enumeration, vulnerability scanning, active exploitation, privilege escalation, and remediation strategies[cite: 8].

---

## Attack Chain Overview & Key Achievements

1. **Reconnaissance & Surface Mapping:**
   - Identified open network services and active operating system details using **Nmap** (`nmap -A`, `nmap -sV`) and automated vulnerability auditing via **Nessus**[cite: 8].
   - Performed web surface enumeration and path brute-forcing utilizing **Gobuster**, **Nikto**, and **WhatWeb**.

2. **Critical Exploitation & Full Compromise:**
   - **OpenSMTPD RCE (CVE-2020-7247):** Leveraged remote code execution to obtain root-level access on the target host.
   - **Log4Shell (CVE-2021-44228):** Executed arbitrary JNDI injection payloads to secure remote command execution (RCE).
   - **Backdoor Shell Access:** Discovered and exploited exposed administrative root backdoors[cite: 8].

3. **Service Enumeration & Password Attacks:**
   - Conducted deep-dive testing across core infrastructure protocols including **FTP**, **Telnet**, and **SMB**[cite: 8].
   - Verified anonymous access vector permissions on FTP servers (`vsftpd` / `ProFTPD`)[cite: 8].
   - Performed dictionary and brute-force credential testing against Telnet instances using **Hydra**.

---

## Summary of High & Critical Findings

| Target Port / Service | Software / Version | CVSS Severity | Key Vulnerability / Vector | Mitigation Strategy |
| :--- | :--- | :---: | :--- | :--- |
| **Port 21 / FTP** | vsftpd 2.3.4[cite: 8] | **Critical**[cite: 8] | Backdoor execution & anonymous access[cite: 8] | Upgrade vsftpd build; disable anonymous access[cite: 8] |
| **Port 23 / Telnet** | Linux telnetd[cite: 8] | **Critical**[cite: 8] | Cleartext transmission / Brute-force risk[cite: 8] | Disable Telnet service; enforce SSH[cite: 8] |
| **Port 25 / SMTP** | OpenSMTPD / Postfix[cite: 8] | **Critical** | RCE (CVE-2020-7247) & weak cipher support[cite: 8] | Apply security patches; enforce TLS 1.2+[cite: 8] |
| **Port 80 / HTTP** | Apache / Log4j[cite: 8] | **Critical** | Log4Shell (CVE-2021-44228) RCE | Update Java libraries; set `-Dlog4j2.formatMsgNoLookups=true` |
| **Port 1524 / Bind Shell**| Root Shell[cite: 8] | **Critical**[cite: 8] | Unauthenticated Root Shell Access[cite: 8] | Terminate rogue process; audit system binaries[cite: 8] |
| **Port 3306 / MySQL** | MySQL 5.0.51a[cite: 8] | **Critical**[cite: 8] | Outdated software, auth-bypass vectors[cite: 8] | Upgrade database engine; restrict remote access[cite: 8] |
| **Port 8180 / Tomcat** | Apache Tomcat 5.5[cite: 8] | **Critical**[cite: 8] | Outdated servlet, default credentials[cite: 8] | Upgrade Tomcat to modern release; harden admin portal[cite: 8] |

---

## Technical Documentation & Artifacts

- [`docs/Vulnerability_Assessment_Report.pdf`](https://github.com/izaan-sh/Web-Server-Penetration-Testing-Assessment/blob/1e835f42ab421c5b9b1faba39a1b767698a88741/docs/Vulnerability%20Assessment%20Report.pdf) — Full technical scan report, port analysis, and mitigation plans[cite: 8].
- [`docs/Penetration_Testing_Assessment.pdf`](./docs/Penetration_Testing_Assessment.pdf) — End-to-end black-box assessment write-up detailing RCE and exploitation vectors.

---

## Environment & Testing Toolkit

* **OS / Environment:** Kali Linux, Target VM Environment[cite: 8]
* **Reconnaissance & Enumeration:** Nmap, Nessus, Gobuster, Nikto, WhatWeb[cite: 8]
* **Exploitation & Cracking:** Metasploit, Hydra, Custom Exploit Scripts
* **Database & Protocol Auditing:** DB Browser, SMBClient, Netcat
