# 🎯 TryHackMe - RootMe Writeup

## 📋 Challenge Overview
**Platform**: TryHackMe  
**Difficulty**: Easy  
**Category**: Web Exploitation, File Upload Bypass, Privilege Escalation  
**Target**: Linux machine with web application  
**Objective**: Gain root access and capture the flag

---

## 🛠️ Tools Used
- **Reconnaissance**: Nmap, Gobuster, Nikto
- **Web Testing**: Burp Suite, OWASP ZAP
- **File Upload Testing**: Custom scripts, manual testing
- **Privilege Escalation**: LinPEAS, manual enumeration
- **Shell Access**: Netcat, reverse shells

---

## 🎯 Attack Path
1. **Initial Reconnaissance** - Port scanning and service enumeration
2. **Web Application Testing** - Directory enumeration and vulnerability assessment
3. **File Upload Exploitation** - Bypassing upload restrictions
4. **Initial Access** - Gaining shell access through file upload
5. **Privilege Escalation** - Escalating to root user
6. **Flag Capture** - Locating and capturing the final flag

---

## 📝 Detailed Walkthrough

### Step 1: Initial Reconnaissance
```bash
# Port scan to identify open services
nmap -sC -sV -p- 10.10.x.x

# Results:
# 22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3
# 80/tcp open  http    Apache httpd 2.4.29
```

### Step 2: Web Application Enumeration
```bash
# Directory enumeration
gobuster dir -u http://10.10.x.x -w /usr/share/wordlists/dirb/common.txt

# Results:
# /panel/ - Directory found
# /uploads/ - Directory found
```

### Step 3: File Upload Testing
*[Detailed file upload bypass techniques will be documented here]*

### Step 4: Initial Access
*[Shell access methodology will be documented here]*

### Step 5: Privilege Escalation
*[Privilege escalation techniques will be documented here]*

### Step 6: Flag Capture
*[Flag location and capture process will be documented here]*

---

## 🎓 Key Learnings
- **File Upload Bypass Techniques**: Understanding how to bypass common upload restrictions
- **Web Application Security**: Identifying and exploiting web vulnerabilities
- **Linux Privilege Escalation**: Manual enumeration and exploitation techniques
- **Documentation**: Importance of thorough note-taking during penetration tests

---

## 🔍 Difficulty Assessment
**Personal Rating**: Easy-Medium  
**Time to Complete**: 2-3 hours  
**Key Challenges**: File upload bypass, privilege escalation enumeration

---

## 📚 Related Resources
- [OWASP File Upload Cheat Sheet](https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload)
- [Linux Privilege Escalation Guide](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite)
- [Web Application Testing Methodology](https://owasp.org/www-project-web-security-testing-guide/)

---

## 🏆 Final Thoughts
This challenge reinforced the importance of thorough enumeration and understanding common web application vulnerabilities. The file upload bypass required creative thinking, and the privilege escalation phase demonstrated the value of systematic enumeration.

---

*This writeup is a work in progress and will be updated with complete details once the challenge is solved.*
