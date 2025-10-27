# Sanjana S  
**Cybersecurity Enthusiast | BCA Graduate | Aspiring Security Analyst**  
🔗 [LinkedIn](https://www.linkedin.com/in/sanjana-s-05b041302) | 📧 sanjanaa.s0607@gmail.com  

---
# 🛡️ Vulnerability Assessment and Penetration Testing (VAPT) – FinTech Web Application

## 📘 Project Overview
This project demonstrates a **Vulnerability Assessment and Penetration Testing (VAPT)** process on a **simulated FinTech web application** hosted in a controlled environment.  
It focuses on identifying security flaws using **manual techniques** and **open-source tools** on **Kali Linux** and **Windows PowerShell**.

---

## 🎯 Objective
To gain hands-on experience in **web application penetration testing** by discovering vulnerabilities and hidden flags within a simulated product website.  
The goal is to understand real-world web security challenges and mitigation strategies without risking real data.

---

## 💡 Problem Statement & Motivation
A FinTech company is preparing to launch a personal finance web app.  
Before going live, a simulated environment was tested to uncover weaknesses such as:
- SQL Injection vulnerabilities  
- Misconfigured login forms  
- Exposed directories and debug files  
- Weak access controls  

This safe testing model ensures that vulnerabilities are found and fixed before production deployment.

---

## 🧰 Tools & Technologies Used
| Tool | Purpose |
|------|----------|
| **Kali Linux** | Platform for ethical hacking and testing |
| **VirtualBox** | Virtual environment for hosting VMs |
| **Nmap** | Network scanning and reconnaissance |
| **Burp Suite** | Web application security testing |
| **Dirb / DirBuster** | Directory brute-forcing |
| **OWASP ZAP** | Automated vulnerability scanning |
| **PowerShell** | File analysis and flag extraction |

---

## ⚙️ Project Setup
1. Imported the vulnerable web application (CTF box) into VirtualBox.  
2. Configured network adapter to allow access from Kali Linux VM.  
3. Used Nmap to discover open ports and services.  
4. Intercepted HTTP traffic with Burp Suite for vulnerability analysis.  
5. Used directory brute-forcing with Dirb/DirBuster to find hidden resources.  
6. Exploited weak inputs manually to capture flags.  
7. Used PowerShell scripts to automate file scanning and extract hidden data.

---

## 💻 PowerShell Code Example

```powershell
$Dest="C:\Users\Administrator\Desktop\Malware_extracted"
$Out="C:\Users\Administrator\Desktop\flag_hits.txt"
$p="(?i)(flag\{[A-Za-z0-9_]+\})"

if (Test-Path $Out) { Remove-Item $Out }

Get-ChildItem $Dest -Recurse -File | ForEach-Object {
    $r=[PSCustomObject]@{Path = $_.FullName}
    $c=[System.IO.File]::ReadAllText($_.FullName, [System.Text.Encoding]::ASCII)
    if ($c -match $p) {
        Add-Content -Path $Out -Value ($Matches[0])
    }
}
