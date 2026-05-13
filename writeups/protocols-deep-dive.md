# 🔐 Protocols Deep Dive: DNS, HTTP & FTP

📍 **Environment:** Kali Linux + Metasploitable2  
🛠️ **Tools:** `dig`, `curl`, Wireshark

---

## 🎯 What I Did Today

### 1. DNS Enumeration with `dig`
- Queried **A records** (IPv4), **NS records** (authoritative nameservers), and **PTR records** (reverse DNS).
- Understood how DNS zone transfers can accidentally expose entire internal infrastructures — a massive recon goldmine in pentests.

### 2. HTTP Request/Response Analysis
- Used `curl -v` to inspect raw headers, check for information leaks, and test **HTTP method support**.
- Customised `User-Agent` and injected `X-Forwarded-For` headers to see how the server reacts (IP spoofing attempts).
- Captured a full HTTP stream in Wireshark and followed the TCP stream to see the plaintext request-response cycle.

### 3. FTP: The Danger of Cleartext
- Connected to **Metasploitable2** via FTP.
- Logged in with `anonymous` access — which was embarrassingly left enabled.
- Started a Wireshark capture, filtered with `ftp`, and **saw the password in plaintext** inside the packet bytes.  
  👁️ *Username and password, visible without any decryption.*

---

## 🧠 Key Takeaways

| Protocol | Risk | Why It Matters |
|----------|------|----------------|
| **DNS** | Zone transfer misconfiguration | Reveals all subdomains, internal IPs, and hostnames — a blueprint for attackers. |
| **HTTP** | Verb tampering (`PUT`, `DELETE`) | Poorly configured servers may allow file uploads or data deletion. |
| **FTP** | No encryption | Credentials travel in cleartext — always sniffable. |
| **vsftpd 2.3.4** | Backdoor vulnerability | Specific version on Metasploitable2 contains a known backdoor (port 6200). |

> 💡 **Core lesson:** If a protocol wasn’t designed with encryption, assume it’s already compromised. Always use encrypted alternatives (HTTPS, SFTP, DoH/DoT).

---

## 📸 Proof of Work

| Screenshot | Description |
|------------|-------------|
| `day06_dig_output.png` | `dig` queries (A, NS, reverse) |
| `day06_curl_http.png` | Verbose HTTP request/response with headers |
| `day06_wireshark_http_stream.png` | Followed HTTP stream in Wireshark |
| `day06_ftp_login.png` | Successful anonymous FTP login |
| `day06_ftp_cleartext_password.png` | Cleartext password visible in Wireshark |

---

## 🔜 Next Steps
- Explore **DNS zone transfer** exploitation (`dig AXFR`)
- Test **HTTP method tampering** with `curl -X PUT`
- Try **vsftpd backdoor exploitation** (with permission on lab)
- Move to **HTTPS/TLS inspection** in Wireshark

---

*Stay curious. Stay ethical. Keep hacking (legally).*  
🕵️‍♂️ #VAPT #CyberSecurity #Wireshark #FTP #DNS
