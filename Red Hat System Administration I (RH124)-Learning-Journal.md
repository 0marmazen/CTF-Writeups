
````markdown
# 🐧 Red Hat Enterprise Linux 9 — Learning Journal  
Student: Omar Mazen  
Field: Computer Engineering — Cybersecurity  
Goal: Documenting my progress and hands-on practice while learning RHEL 9  
````


## CH01 — Install RHEL 9 Step by Step

###  Install RHEL 9   
> 
---

## CH02 — Accessing the Command Line
### Lesson 1 — Intro  
>Introduction to the Linux command line (CLI). It’s the main way to interact with the system, letting you control almost everything using simple commands.
### Lesson 2 — What is Bash Shell
>Bash is the program that executes the commands you type in the terminal. It interprets your input so the system can understand and run it.
### Lesson 3 — Command Syntax
>Every Linux command has a structure: command [options] [arguments].
Example: ls -l /home lists files in detail.
### Lesson 4 — How to Access the CLI
>You can open the terminal via the application or Ctrl+Alt+T. You can work as a regular user or as root depending on what you need.
### Lesson 5 — Date, Passwd and File Commands
>Important commands: date shows the current date/time, passwd changes your password, ls, cp, mv, rm manage files.
### Lesson 6 — Cat vs Less vs Head and Tail
>cat shows the whole file, less shows it page by page, head shows the first 10 lines, tail shows the last 10 lines and can follow updates.
### Lesson 7 — History Command
>history shows your previously executed commands, useful for repeating or reviewing commands.
### Lesson 8 — Shell Shortcuts
>Key shortcuts: Ctrl+C stops a running command, Ctrl+R searches command history, Tab auto-completes commands or filenames.
> ![Shell Shortcuts](assets/RHEL/1.png)
```BASH
hat@192:~$ ls | grep my
myfoldeer
myfoldeesr
myfolder
hat@192:~$ mkdir myF\
> cd myF\
> touch F1.txt F2.txt
hat@192:~$ 

```
---

## CH03 — Managing Files From the Command Line
### Lesson 1 — Access Linux File System  
> ![Linux File System](assets/RHEL/2.png)
### Lesson 2 — Major Directories  

| **Path** | **Description**                                                                                       |
| -------- | ----------------------------------------------------------------------------------------------------- |
| `/`      | Root directory, contains essential files for booting and other filesystems mounted as subdirectories. |
| `/bin`   | Essential command binaries.                                                                           |
| `/boot`  | Bootloader, kernel, and files needed to boot Linux.                                                   |
| `/dev`   | Device files for accessing hardware devices.                                                          |
| `/etc`   | Local system configuration files and installed application configs.                                   |
| `/home`  | Users' personal directories.                                                                          |
| `/lib`   | Shared libraries required for system boot.                                                            |
| `/media` | Mount point for external removable media (USB, CD, etc.).                                             |
| `/mnt`   | Temporary mount point for filesystems.                                                                |
| `/opt`   | Optional files, like third-party tools.                                                               |
| `/root`  | Root user's home directory.                                                                           |
| `/sbin`  | System administration executables.                                                                    |
| `/tmp`   | Temporary files, usually cleared on boot.                                                             |
| `/usr`   | User applications, binaries, libraries, and man files.                                                |
| `/var`   | Variable data like logs, emails, web files, cron jobs, etc.                                           |

### Lesson 3 — Linux File Types  
| **Symbol** | **Meaning**                                        |
| ---------- | -------------------------------------------------- |
| `-`        | Regular file|
| `d`        | Directory|
| `l`        | Symbolic link (shortcut)|
| `c`        | Character device file (in `/dev`)|
| `b`        | Block device file (e.g., hard drives, disk images) |
| `s`        | Socket      |
| `p`        | Named pipe (FIFO)           |



### Lesson 4 — Naming Rules  
| **Linux File Names** | **Should**                                 | **Should Not**                              |
| -------------------- | -------------------------------------------- | --------------------------------------------------|
| Naming rules | Be descriptive| Include embedded blanks|
| Characters | Only alphanumeric characters (UPPERCASE, lowercase, numbers, @, _) | Contain shell metacharacters `* ? > < / ; & ! [ ] \ ‘ “ ( ) { }` |
| Case sensitivity| Are case sensitive| —|
| Hidden files| Filenames starting with `.` are hidden|—|
| Length| Maximum number of characters for a filename is 255| —|

### Lesson 5 — Absolute vs Relative Path  
> 
### Lesson 6 — LS Command  
| **Option**  | **Description**                                                                                                                      |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `-l`        | Long list format. Shows file permissions, number of links, owner, group, file size, last modification time, and file/directory name. |
| `-lh`       | Long list format with **human-readable file sizes** (e.g., KB, MB).                                                                  |
| `-r`        | Lists files in **reverse order**.                                                                                                    |
| `-a`        | Shows **all files**, including hidden files (those starting with `.`).                                                               |
| `-ltr`      | Combines options: **long format, sort by time**, and **reverse order**. Shows the latest modifications last.                         |
| `-F`        | Adds a **trailing `/` for directories**, `*` for executable files, etc.                                                              |
| `-lS`       | Long format, **sorted by size** (largest to smallest).                                                                               |
| `-R`        | Recursively lists **all directories and subdirectories**.                                                                            |
| `-i`        | Displays **inode numbers** beside files and directories.                                                                             |
| `dir`        | The dir command is similar to `ls` and can be used in Linux to list files and directories. It supports the same options as `ls`.     |
| `man ls`    | Opens the **manual page** for `ls`, showing all options and details.                                                                 |

> 
### Lesson 7 — Managing Files  
> 
### Lesson 8 — Create & Copy Files  
|ACTIVITY | COMMAND SYNTAX |
|-|-|
|Create a directory | mkdir directory|
|Copy a file|`cp file new-file`|
|Copy a directory and its contents|`cp -r directory new-directory`|
|Move or rename a file or directory|`mv file new-file`|
|Remove a file|`rm file`|
|Remove a directory containing files|`rm -r directory`|
|Remove an empty directory|`rmdir directory`|
### Lesson 9 — Move & Remove Files  
> 
### Lesson 10 — Hard Links vs Soft Links  
> 🧱 Hard link = another name for the same file (`same data`).
> 🔗 Soft link = a pointer or `shortcut` to the original file.
### Lesson 11 — Linux Inodes  
> 
### Lesson 12 — Creating Links (Part 1)  
> 
### Lesson 13 — Creating Links (Part 2)  
> 
### Lesson 14 — Pattern Matching  
> 
### Lesson 15 — Grep Command  
> 
### Lesson 16 — Regular Expressions with Grep  
> 
### Lesson 17 — Cut and Tr Commands  
> 

---

## CH04 — Getting Help in RHEL
### Lesson 1 — Intro  
> 
### Lesson 2 — Manual Pages Overview  
> 
### Lesson 3 — man Command  
> 
### Lesson 4 — Search Patterns in Manual Pages  
> 
### Lesson 5 — Other Ways to Get Help  
> 
### Lesson 6 — Summary  
> 

---

## CH05 — Creating, Viewing, and Editing Text Files
### Lesson 1 — Intro  
> 
### Lesson 2 — Input Output Redirection  
> 
### Lesson 3 — Piping in Linux  
> 
### Lesson 4 — VIM Editor Modes  
> 
### Lesson 5 — Command & Insert Modes  
> 
### Lesson 6 — Extended & Visual Modes  
> 
### Lesson 7 — VIM Cheat Sheet  
> 
### Lesson 8 — User-Defined Variables  
> 
### Lesson 9 — Shell Variables (Part 1)  
> 
### Lesson 10 — Shell Variables (Part 2)  
> 
### Lesson 11 — Shell Variables (Part 3)  
> 
### Lesson 12 — Set & Unset Permanent Variables  
> 
### Lesson 13 — Summary  
> 

---

## CH06 — Managing Local Users and Groups
### Lesson 1 — Intro  
> 
### Lesson 2 — User Identifier (UID)  
> 
### Lesson 3 — Group Identifier (GID)  
> 
### Lesson 4 — SU vs SUDO Commands  
> 
### Lesson 5 — Grant Superuser Access  
> 
### Lesson 6 — Create, Modify, Delete Users  
> 
### Lesson 7 — Create, Modify, Delete Groups  
> 
### Lesson 8 — Change User Password Params  
> 
### Lesson 9 — Restrict User Access  
> 
### Lesson 10 — Summary  
> 

---

## CH07 — Controlling Access to Files
### Lesson 1 — Intro  
> 
### Lesson 2 — File System Permissions  
> 
### Lesson 3 — Change Permissions (Symbolic)  
> 
### Lesson 4 — Change Permissions (Numeric)  
> 
### Lesson 5 — Ownership  
> 
### Lesson 6 — Special Permissions (Setuid, Setgid, Sticky)  
> 
### Lesson 7 — Default File Permissions  
> 
### Lesson 8 — Summary  
> 

---

## CH08 — Monitoring and Managing Processes
### Lesson 1 — Intro  
> 
### Lesson 2 — List Running Processes  
> 
### Lesson 3 — Manage Foreground & Background  
> 
### Lesson 4 — Kill Signals  
> 
### Lesson 5 — Top Command  
> 
### Lesson 6 — Process Priority  
> 
### Lesson 7 — Summary  
> 

---

## CH09 — Controlling Services and Daemons
### Lesson 1 — Intro  
> 
### Lesson 2 — Check Service Status  
> 
### Lesson 3 — Manage Services  
> 
### Lesson 4 — Summary  
> 

---

## CH10 — Configuring and Securing SSH
### Lesson 1 — Intro  
> 
### Lesson 2 — Access Remote CLI with SSH  
> 
### Lesson 3 — Configure SSH Key Authentication  
> 
### Lesson 4 — Customize SSH Service Config  
> 
### Lesson 5 — Summary  
> 

---

## CH11 — Analyzing and Storing Logs
### Lesson 1 — Intro  
> 
### Lesson 2 — System Log Architecture  
> 
### Lesson 3 — Review Syslog Files  
> 
### Lesson 4 — Preserve systemd Journal  
> 
### Lesson 5 — Change Timezone  
> 
### Lesson 6 — Summary  
> 

---

## CH12 — Managing Networking
### Lesson 1 — Intro  
> 
### Lesson 2 — Validate Network Config  
> 
### Lesson 3 — Configure Networking  
> 
### Lesson 4 — Modify Network Files  
> 
### Lesson 5 — Configure Hostnames  
> 
### Lesson 6 — Summary  
> 

---

## CH13 — Archiving and Transferring Files
### Lesson 1 — Intro  
> 
### Lesson 2 — Manage Tar Archives  
> 
### Lesson 3 — Transfer Files Securely  
> 
### Lesson 4 — Summary  
> 

---

## CH14 — Installing and Updating Software
### Lesson 1 — Intro  
> 
### Lesson 2 — RPM Packages Overview  
> 
### Lesson 3 — Download RPM Package  
> 
### Lesson 4 — Examine RPM Packages  
> 
### Lesson 5 — Install Packages with rpm  
> 
### Lesson 6 — Yum Repositories  
> 
### Lesson 7 — Create Yum Repo  
> 
### Lesson 8 — List/Search/Install with YUM  
> 
### Lesson 9 — Update/Remove Packages with YUM  
> 
### Lesson 10 — Summary  
> 

---

## CH15 — Accessing Linux File Systems
### Lesson 1 — Intro  
> 
### Lesson 2 — Examine File Systems  
> 
### Lesson 3 — Mount & Unmount File Systems  
> 
### Lesson 4 — Search Files on Mounted FS  
> 
### Lesson 5 — Summary  
> 
```

---



## 📊 Summary

| Chapter | Title          | Status| Notes                         |
| ------- | -------------- |:----:| ----------------------------- |
| CH01    | Install RHEL 9 |   ✅  | Installed on VirtualBox       |
| CH02    | Command Line   |    ✅   | Practiced basic commands      |
| CH03    | Managing Files |    -   | Learned links and paths       |
| CH04    | Help in RHEL   |       | Used `man` and `--help`       |
| CH05    | Editing Text   |       | Practiced Vim and redirection |
| CH06    | Users & Groups |       | Managed users & permissions   |
| CH07    | File Access    |       | Learned chmod/chown           |
| CH11    | Logs           |       | Used journalctl               |
| CH12    | Networking     |       | Set IP and hostname           |
| CH14    | Packages       |       | Installed via yum             |

---

🕓 **Last Updated:** November 2025
📘 **Maintained by:** Omar Mazen
🔥 *Learning by doing — every command counts!*

```

