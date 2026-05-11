# 🕵️ Network Enumeration & Traffic Analysis

## Target
- Local Lab Environment

---

## Finding Title
**Information Disclosure via Unencrypted HTTP Traffic and Stealth Port Scanning**

---

## Description
Analyzing network traffic during a communication session revealed that data sent over HTTP is transmitted in plaintext, allowing an attacker to intercept sensitive information.  
Additionally, Stealth SYN scanning was used to map open ports while bypassing basic logging mechanisms.

---

## Step-by-Step Reproduction
1. **Packet Sniffing**  
   - Start Wireshark on the primary interface and filter for `http` or `tcp.flags.syn == 1`.  
2. **Stealth Scanning**  
   - Execute an Nmap SYN scan to identify open ports without completing the 3-way handshake:  
     ```bash
     sudo nmap -sS -Pn [192.162.x.x]
     ```  
3. **Traffic Inspection**  
   - Right-click a TCP stream in Wireshark and select **Follow > TCP Stream** to view the raw data exchange.  

---

## Expected vs Actual Result
- **Expected:**  
  - Network traffic should be encrypted (HTTPS/TLS).  
  - Scanning attempts should be blocked or logged by a firewall.  

- **Actual:**  
  - Sensitive data was visible in plaintext via Wireshark.  
  - Nmap successfully identified open ports (80, 443, etc.) using half-open connections.  

---

## Proof / Screenshot
![Wireshark Traffic Analysis](https://github.com/kumar428/cybersecurity-portfolio/raw/main/assets/wireshark_traffic.png)  


---

## Impact (CVSS Score)
**5.3 (Medium)**  
`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N`  

- Lack of encryption allows for sniffing/MITM attacks.  
- Stealth scanning facilitates reconnaissance.  

---

## Remediation
- **Enforce Encryption:** Transition all web traffic from HTTP to HTTPS using strong TLS (1.2 or 1.3) certificates.  
- **Firewall Hardening:** Configure Firewall/IDS to detect and block rapid SYN packets.  
- Implement rate-limiting to prevent stealthy reconnaissance.  
