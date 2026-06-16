# Penetration Test Report  – Metasploitable 2 Exploitation

This directory contains the full-cycle penetration testing report for the Metasploitable 2 target within my home lab environment. The assessment follows the PTES methodology, covering reconnaissance, enumeration, exploitation, and post-exploitation.

## Engagement Summary
- **Target:** Metasploitable 2 (192.168.1.21) – intentionally vulnerable Linux server
- **Attacker:** Kali Linux (192.168.1.242)
- **Key Vulnerability:** vsftpd 2.3.4 backdoor (CVE-2011-2523)
- **Exploitation:** Metasploit `vsftpd_234_backdoor` module with Meterpreter payload
- **Result:** Root-level remote shell obtained

## What's Inside
- Network discovery and service enumeration (Nmap)
- Vulnerability identification and exploit selection
- Metasploit payload configuration and execution
- Post-exploitation actions: system info, credential access, network recon
- Remediation recommendations

## Full Report
The complete, professional penetration test report is available as a PDF:

📄 [Download Penetration Test Report (PDF)](./Report_2_Penetration_Test.pdf)

*(The PDF includes screenshots of all terminal outputs, Meterpreter sessions, and root compromise evidence.)*

---

**Author:** Kumar Palanivelu | Portfolio Project  
