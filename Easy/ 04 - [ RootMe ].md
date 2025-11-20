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

The upload form blocks `.php` files but accepts alternative P
