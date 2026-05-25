# 🔐 Metasploit Framework Basics

📍 **Environment:** Kali Linux attacking Metasploitable2  
🛠️ **Tools:** Metasploit Framework (msfconsole)

---

## 🎯 What I Did Today

### 1. Started msfconsole & Explored the Interface
- Launched `msfconsole` and explored the command set: `search`, `use`, `show options`, `back`, `info`.
- Understood the modular structure: exploits, payloads, auxiliary, post, encoders, nops.
- Searched for modules related to Metasploitable2 (`vsftpd`, `samba`).

### 2. Exploited vsftpd 2.3.4 Backdoor
- Used the `exploit/unix/ftp/vsftpd_234_backdoor` module.
- Set `RHOSTS` to the target IP and ran the exploit.
- Got an immediate root shell — no privilege escalation required.  
  *This backdoor was introduced by an attacker who compromised the vsftpd source code.*

### 3. Configured a Multi/Handler Listener
- Set up a generic reverse TCP listener with `exploit/multi/handler`.
- Configured `PAYLOAD` as `linux/x86/meterpreter/reverse_tcp`, set `LHOST`, and waited for incoming connections.
- Demonstrated that Metasploit can catch shells from any custom exploit or payload.

### 4. Ran an Auxiliary TCP Port Scanner
- Used `auxiliary/scanner/portscan/tcp` to scan common ports on the target.
- Set `RHOSTS`, `PORTS`, and ran the scan. Observed open ports: 21 (FTP), 22 (SSH), 23 (Telnet), 80 (HTTP), 139/445 (Samba), 3306 (MySQL), etc.
- Auxiliary modules provide reconnaissance without triggering an exploit.

### 5. Post-Exploitation Recon
- On the vsftpd root shell, ran commands: `id`, `uname -a`, `ifconfig`, `cat /etc/passwd`, `cat /etc/shadow`.
- Identified the kernel version and looked for local privilege escalation paths (not needed here).
- Documented the host information for reporting.

### 6. Researched Another Module: samba/usermap_script
- `search samba` returned `exploit/multi/samba/usermap_script`.
- Studied the module info (`info`) and understood it exploits a command injection vulnerability in Samba 3.0.20.
- Confirmed Metasploitable2 runs this version — a second reliable root exploit ready to use.

---

## 🧠 Key Takeaways

| Concept | Why It Matters |
|---------|----------------|
| **Modular design** | Exploits, payloads, auxiliary modules are interchangeable — mix and match for flexibility |
| **vsftpd backdoor** | Classic example of a supply-chain attack — always works for practice |
| **multi/handler** | Essential for catching shells from any source, not just Metasploit modules |
| **Auxiliary scanners** | Perform reconnaissance without exploitation — safe for production |
| **Post-exploitation** | Once you have a shell, recon the host for credentials, networks, and escalation paths |
| **Module info** | Always `info` a module before running — understand what it does and its requirements |

> 💡 **Core lesson:** Metasploit isn't just a click-to-exploit tool. It's a modular framework that supports every phase of a penetration test — from scanning to exploitation to post-exploitation. Mastering it means you can quickly validate vulnerabilities, deliver payloads, and document findings.

---
## 📸 Proof of Work

| Screenshot | Description |
|:---|:---|
| ![Metasploit Scanner](https://raw.githubusercontent.com/kumar428/cybersecurity-portfolio/main/assets/VirtualBox_kali%20Linux_25_05_2026_20_53_08.png) |  Running the auxiliary port scanner module against the Metasploitable2 target |
| ![vsftpd Exploit](https://raw.githubusercontent.com/kumar428/cybersecurity-portfolio/main/assets/VirtualBox_kali%20Linux_25_05_2026_20_53_44.png) |  Executing the vsftpd 2.3.4 backdoor exploit and gaining immediate root access |
