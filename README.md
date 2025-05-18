# Gamma Ethical Hacking CTF Write-up

## 📁 Project Overview

This repository contains a detailed write-up of a multi-stage ethical hacking Capture the Flag (CTF) simulation targeting a hybrid enterprise network. The report demonstrates realistic attack chains across Windows Active Directory infrastructure and Linux servers. The objective was to gain initial access, escalate privileges, perform credential harvesting, and evaluate the environment’s security posture through practical, real-world techniques.

---

## 🖥️ Target Environment

The simulated environment included:

- **Windows Active Directory Domain Controller**  
- **Two Domain-Joined Windows Hosts (Box A & Box B)**  
- **A Standalone Linux Server Running Joomla CMS**  

These machines formed a realistic enterprise network with domain-linked users, misconfigurations, vulnerable services, and exploitable attack paths.

---

## 🛠️ Methodology

The engagement followed a structured red-team/penetration testing approach across multiple platforms:

- **Reconnaissance & Enumeration**  
  - Network and host discovery using tools like `nmap`, `arp-scan`, and `netdiscover`  
  - User, group, and share enumeration via `CrackMapExec`, `rpcclient`, and `smbclient`  
  - Active Directory mapping using `BloodHound` and `bloodhound-python`  
  - Web enumeration and analysis with `Dirsearch`, `JoomScan`, `Burp Suite`, and `CeWL`

- **Initial Access & Exploitation**  
  - Gaining access through weak credentials, misconfigured services, or vulnerable web apps  
  - Joomla admin panel compromise via brute-force with custom wordlists  
  - Remote shell access using tools like `impacket-psexec`, `wmiexec`, and custom PHP reverse shells

- **Privilege Escalation**  
  - On Windows: exploiting service misconfigurations (e.g., unquoted paths, writable registries), DLL hijacking, scheduled tasks, and AlwaysInstallElevated  
  - On Linux: leveraging `sudo` misconfigurations, weak PATH controls, insecure cron jobs, and exposed scripts or credentials

- **Credential Attacks**  
  - Dumping credentials with `Mimikatz`, `hashdump`, and `secretsdump.py`  
  - Performing offline cracking with `Hashcat` and `John the Ripper`  
  - Extracting GPP-stored passwords and performing AS-REP Roasting & Kerberoasting via `Impacket`

- **Post-Exploitation**  
  - Establishing NT AUTHORITY\SYSTEM shells  
  - Lateral movement across domain-joined systems  
  - Domain controller compromise and golden ticket generation  
  - Full flag collection and documentation of persistence techniques


## 🔍 Key Techniques & Findings

| Category                | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| **Active Directory**    | BloodHound analysis, Kerberoasting, DCSync, golden tickets                  |
| **Credential Harvesting** | NTLM hashdump, Mimikatz, AS-REP roasting, GPP password discovery         |
| **Privilege Escalation** | Service misconfigurations, writable registry keys, unquoted service paths |
| **Linux Exploits**      | Joomla RCE via template injection, sudo ALL access, credential reuse        |
| **Web Attack Surface**  | Joomla brute-force via CeWL + Burp, PHP reverse shell upload                |
| **Post-Exploitation**   | SYSTEM-level access, persistence paths, full domain takeover                |

---

## 🧰 Some of the Tools Used

| Tool                    | Purpose                                   |
|-------------------------|-------------------------------------------|
| Nmap, ARP-scan          | Network scanning and discovery            |
| CrackMapExec, rpcclient| SMB & RPC enumeration                     |
| BloodHound              | Active Directory attack path analysis     |
| Impacket (psexec, wmiexec, secretsdump) | Remote shell, hashdump, domain sync |
| Mimikatz                | Credential dumping                        |
| Hashcat, John the Ripper| NTLM/Kerberos hash cracking               |
| Burp Suite, Dirsearch   | Web app brute-force and directory scan    |
| CeWL, Hydra             | Wordlist generation and login attempts    |
| WinPEAS, LinPEAS        | Local privilege escalation discovery      |
| Metasploit              | Exploitation and session management       |
| Nessus                  | Vulnerability scanning                    |

---

## 📑 Report Contents

| Section                        | Highlights                                                                 |
|--------------------------------|---------------------------------------------------------------------------|
| Executive Summary              | High-level overview of goals, scope, and outcomes                         |
| First Goal: Acquiring Access   | Domain and local privilege escalation across Windows and Linux targets    |
| Second Goal: Attack Vectors    | Credential dumping, Kerberoasting, AS-REP Roasting, Golden Ticket attacks |
| Remediation                    | Detailed Windows and Linux hardening recommendations                      |
| Contributions                  | Summary of each participant’s role and tasks                             |
| References                     | Tools, resources, and external write-ups used during the challenge        |


---

## 📘 License

This repository is provided for academic and educational use only. Reuse or redistribution requires proper attribution and permission.

