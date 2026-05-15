# 🔐 Linux Privilege Escalation Techniques

📍 **Environment:** Kali Linux (simulated)  
🛠️ **Tools:** `sudo`, `find`, `vim`, `openssl`, `john`, `nc`

---

## 🎯 What I Did Today

### 1. Kernel Exploit Recon
- Ran `uname -a` and `searchsploit` to check kernel version.
- Understood that kernel exploits can crash production systems, so they’re last resort in a real pentest.

### 2. Sudo Misconfiguration Abuse
- Created a low-priv user and granted `NOPASSWD: /usr/bin/find`.
- Switched to that user and ran `sudo find . -exec /bin/bash \;` → instant root shell.
- Demonstrated why `sudo -l` is always the first command after a foothold.

### 3. Cron Job Hijack
- Added a root cron job that executed a world-writable script (`/tmp/cleanup.sh`).
- Injected a reverse shell into that script.
- Set up a netcat listener and received a root shell within one minute.

### 4. Writable `/etc/passwd`
- Simulated a misconfigured world-writable `/etc/passwd`.
- Generated a password hash with `openssl` and appended a new root-equivalent user.
- Logged in as the new user and confirmed `whoami` returns root.

### 5. Readable `/etc/shadow`
- Made `/etc/shadow` world-readable to simulate a misconfiguration.
- Extracted the root hash and started cracking with `john` and the rockyou wordlist.
- Learned how even a simple misstep can expose all credentials.

### 6. SUID Vim Escape
- Located a SUID `vim` binary with `find / -perm -4000`.
- Escaped to a shell using `vim -c ':!/bin/bash'` – immediate root access.

---

## 🧠 Key Takeaways

| Technique | Risk | Why It Matters |
|-----------|------|----------------|
| **Sudo misconfig** | `NOPASSWD` on dangerous binaries | Single command gives root instantly |
| **SUID binaries** | Uncommon SUID on `vim`, `find`, `bash` | Escalation without passwords |
| **Cron jobs** | Writable scripts called by root | Reverse shell or command injection |
| **/etc/passwd writable** | Anyone can add a root user | Full compromise, no exploit needed |
| **/etc/shadow readable** | Hashes exposed | Offline cracking can reveal passwords |
| **Kernel exploits** | Old unpatched kernel | Can give root but may crash the system |

> 💡 **Core lesson:** Privilege escalation is not about luck – it’s about systematically checking every weak permission, misconfiguration, and accessible sensitive file. In 90% of cases, `sudo -l`, SUID hunt, and file permission checks are enough.

---

## 📸 Proof of Work

| Screenshot | Description |
|------------|-------------|
| `day08_kernel_recon.png` | `uname -a`, `searchsploit` output |
| `day08_sudo_abuse.png` | `sudo -l` and root shell via `find` |
| `day08_cron_hijack.png` | Reverse shell listener caught root shell |
| `day08_writable_passwd.png` | New root user added to `/etc/passwd` |
| `day08_readable_shadow.png` | Root hash extraction and `john` cracking |
| `day08_suid_vim.png` | Root shell via SUID `vim` escape |
