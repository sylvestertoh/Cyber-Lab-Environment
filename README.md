# 🛡️ Cybersecurity Home Lab & Project Portfolio

## 📍 Project Overview
This repository documents my journey in building a professional-grade cybersecurity laboratory focused on **Reverse Engineering** and **Penetration Testing**. My goal is to demonstrate technical proficiency and a structured methodology suitable for entry-level cybersecurity roles in Singapore.

## 🧪 Phase 1: Lab Architecture (Current)
To ensure high performance and tool stability, I have opted for a **Type-2 Hypervisor** setup with hardware-level optimizations.

- **Hypervisor:** VMware Workstation Pro 25H2u1
- **Host Optimization:** Disabled Windows Hyper-V (`bcdedit /set hypervisorlaunchtype off`) to allow raw VT-x access for the hypervisor, ensuring 100% performance for debuggers and specialized RE tools.
- **Primary Attacker:** Kali Linux 
- **Primary RE Target:** Windows 10 Pro

## 📁 Repository Structure
- `/Scans`: Configuration scripts and results.
- `/Reverse-Engineering`: Write-ups and analysis of binaries and malware samples.
- `/Penetration-Testing`: Documented exploit chains and network assessments.
- `/Automation`: Python and Bash scripts developed for security task automation.

## 🚀 About Me
- **Education:** B.Sc. in Cybersecurity
- **Current Focus:** Building a reverse engineering portfolio and learning the Singapore threat landscape. Hope to enter into the Cybersecurity field.
- Currently Employed as an **Application Development Engineer** 


![Kali](https://img.shields.io/badge/OS-Kali_Linux-blue?logo=kalilinux&logoColor=white) 
![VMware](https://img.shields.io/badge/Lab-VMware_Workstation-orange?logo=vmware&logoColor=white) 
![Python](https://img.shields.io/badge/Scripting-Python-3776AB?logo=python&logoColor=white)

## 🚩 Progress Log

### Phase 1: Network & OS Initialization
- [x] Deployed **Kali Linux 2026.1** as the primary Attacker Node.
- [x] Hardened the environment with `full-upgrade`.
- [x] Provisioned **Windows 10 Enterprise (22H2)** as the Victim Node.
- [x] Configured **Host-Only networking** to ensure 100% lab isolation.

### Phase 2: Network Discovery & Reconnaissance
- [x] Assigned Static IP `192.168.164.50` to the Windows Target.
- [x] Verified connectivity between nodes via ICMP (Ping).
- [x] Conducted an **Aggressive Nmap Scan (`-A`)** to identify open services (SMB, RDP, RPC).**Nmap Scan Results:** [View raw scan output](./Scans/nmap_windows_victim.txt)

### Phase 3: Vulnerability Assessment (NSE)
**Command:** `sudo nmap --script vuln 192.168.164.50` **Vuln Scan Results:** [View raw scan output](./Scans/vuln_scan_results.txt)

**Technical Analysis:**
- **Surface Area:** Ports 135, 139, and 445 (SMB/RPC) were confirmed open. This represents a standard Windows management surface.
- **Vulnerability Status:** Initial NSE scripts for legacy exploits (MS10-061, MS10-054) returned negative or inconclusive results. 
- **Conclusion:** The target (Windows 10 22H2) appears to have modern security patches applied, successfully mitigating common legacy SMB-based exploits.
- 
### Phase 4: Active Reconnaissance (Metasploit)
Used the Metasploit Framework (MSF) to verify target configurations.

- **Module:** `auxiliary/scanner/smb/smb_version`
- **Finding:** Verified Target OS as Windows 10 Pro.
- **Security Check:** Attempted `smb_login` with common weak credentials. 
- **Result:** Login Failed (Expected behavior for a secure local account).
