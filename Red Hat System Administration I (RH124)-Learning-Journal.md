
````markdown
# 🐧 Red Hat Enterprise Linux 9 — Learning Journal  
**Student:** Omar Mazen  
**Field:** Computer Engineering — Cybersecurity  
**Goal:** Documenting my progress and hands-on practice while learning RHEL 9  
````
## 🧩 CH01 — Install RHEL 9 Step by Step

### 🎯 Objectives
- Understand what Linux and RHEL are.
- Learn installation requirements and system setup.

### 🧠 Notes
- RHEL = Red Hat Enterprise Linux (enterprise-grade distro).
- Installation requires ≥ 2 GB RAM and 20 GB disk.
- Tools used: VirtualBox / VMware.

### 🧰 Commands & Practice
```bash
# Check system info
uname -a

# List disks before installation
lsblk


### ✅ Status

✔️ Completed — Successfully installed RHEL 9 on VirtualBox.

---

## 💻 CH02 — Accessing the Command Line

### 🎯 Objectives

* Learn Bash shell basics.
* Understand command syntax and navigation.

### 🧠 Notes

* Bash = Bourne Again Shell.
* Command format: `command [options] [arguments]`
* `history` shows last executed commands.

### 🧰 Commands & Practice

```bash
pwd        # show current directory
ls -l      # list files with details
cd /etc    # move to etc directory
history    # list past commands
```

### ✅ Status

✔️ Completed — Practiced CLI navigation and command history.

---

## 📁 CH03 — Managing Files From the Command Line

### 🎯 Objectives

* Manage directories and files via terminal.
* Learn paths, file types, and symbolic vs hard links.

### 🧠 Notes

* Absolute path: starts from root `/`
* Relative path: based on current directory
* Hard link = direct pointer to inode
* Soft link = shortcut to another file

### 🧰 Commands & Practice

```bash
touch file1.txt
cp file1.txt backup.txt
mv backup.txt /tmp/
ln file1.txt link1
ln -s /tmp/backup.txt softlink
```

### ✅ Status

✔️ Completed — Practiced linking, copying, moving, and deleting files.

---

## 🧑‍💻 CH04 — Getting Help in RHEL

### 🎯 Objectives

* Learn to use manual pages and help commands.

### 🧠 Notes

* `man command` → open manual page.
* Use `/keyword` inside man to search.
* Short help → `command --help`

### 🧰 Commands

```bash
man ls
ls --help
man -k network
```

### ✅ Status

✔️ Completed — Confident using man pages.

---

## 📝 CH05 — Creating, Viewing, and Editing Text Files

### 🎯 Objectives

* Learn redirection, piping, and editing text with Vim.

### 🧠 Notes

* `>` redirects output to file.
* `|` pipes one command’s output to another.
* Vim modes: normal, insert, visual.

### 🧰 Commands

```bash
echo "Hello Linux" > hello.txt
cat hello.txt | grep "Linux"
vim notes.txt
```

### ✅ Status

✔️ Completed — Created and edited files in Vim.

---

## 👤 CH06 — Managing Local Users and Groups

### 🎯 Objectives

* Create, modify, and delete users/groups.
* Understand UID/GID and permissions.

### 🧠 Notes

* Superuser access with `sudo` or `su`.
* `/etc/passwd` and `/etc/group` store user info.

### 🧰 Commands

```bash
sudo adduser testuser
sudo passwd testuser
sudo usermod -aG sudo testuser
sudo deluser testuser
```

### ✅ Status

✔️ Completed — Practiced managing local accounts.

---

## 🔐 CH07 — Controlling Access to Files

### 🎯 Objectives

* File permissions, ownership, and special bits.

### 🧠 Notes

* Permissions: r (4), w (2), x (1)
* Numeric example: 755 = rwxr-xr-x
* Sticky bit prevents deletion by others.

### 🧰 Commands

```bash
chmod 755 script.sh
chown omar:omar script.sh
ls -l
```

### ✅ Status

✔️ Completed — Practiced file permission management.

---

## 🧾 CH11 — Analyzing and Storing Logs

### 🎯 Objectives

* Understand Linux logging system.

### 🧠 Notes

* Logs stored in `/var/log`
* `journalctl` for systemd logs

### 🧰 Commands

```bash
cd /var/log
cat messages
journalctl -xe
```

### ✅ Status

✔️ Completed — Reviewed and analyzed log files.

---

## 🌐 CH12 — Managing Networking

### 🎯 Objectives

* Configure IP, DNS, and hostname.

### 🧠 Notes

* Config files in `/etc/sysconfig/network-scripts/`
* Use `nmcli` or `nmtui` for management.

### 🧰 Commands

```bash
ip a
nmcli dev show
hostnamectl set-hostname rhel9lab
```

### ✅ Status

✔️ Completed — Configured static IP and hostname.

---

## 📦 CH14 — Installing and Updating Software Packages

### 🎯 Objectives

* Use `rpm` and `yum` to install/manage packages.

### 🧠 Notes

* `rpm -i` install, `rpm -e` remove.
* `yum` handles dependencies automatically.

### 🧰 Commands

```bash
sudo yum install httpd -y
rpm -qa | grep httpd
sudo systemctl start httpd
```

### ✅ Status

✔️ Completed — Installed Apache server successfully.

---

## 📊 Summary

| Chapter | Title          | Status | Notes                         |
| ------- | -------------- | :----: | ----------------------------- |
| CH01    | Install RHEL 9 |    ✅   | Installed on VirtualBox       |
| CH02    | Command Line   |    ✅   | Practiced basic commands      |
| CH03    | Managing Files |    ✅   | Learned links and paths       |
| CH04    | Help in RHEL   |    ✅   | Used `man` and `--help`       |
| CH05    | Editing Text   |    ✅   | Practiced Vim and redirection |
| CH06    | Users & Groups |    ✅   | Managed users & permissions   |
| CH07    | File Access    |    ✅   | Learned chmod/chown           |
| CH11    | Logs           |    ✅   | Used journalctl               |
| CH12    | Networking     |    ✅   | Set IP and hostname           |
| CH14    | Packages       |    ✅   | Installed via yum             |

---

🕓 **Last Updated:** November 2025
📘 **Maintained by:** Omar Mazen
🔥 *Learning by doing — every command counts!*

```

