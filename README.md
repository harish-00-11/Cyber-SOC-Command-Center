# ⚡ Cyber SOC Command Center

A real-time Security Operations Center (SOC) dashboard built using Splunk SIEM to monitor, detect, and analyze cyber attacks in a home lab environment.

This project simulates real-world SOC operations including:
- Brute force attack detection
- RDP attack monitoring
- Failed & successful login tracking
- Privilege escalation monitoring
- Lateral movement detection
- PowerShell abuse detection
- Threat intelligence visualization
- MITRE ATT&CK mapping

---

# 📌 Features

## 🔍 Real-Time Monitoring
- Failed login attempts (Event ID 4625)
- Successful logins (Event ID 4624)
- RDP login detection
- Account lockout monitoring
- NTLM authentication failures
- Privilege escalation alerts

## 🚨 Threat Detection
- Brute force attack detection
- Suspicious PowerShell execution
- Pass-the-Hash indicators
- Lateral movement monitoring
- Credential access activity
- Sysmon process monitoring

## 📊 Dashboard Visualizations
- Threat severity overview
- Attack timelines
- Global attack map
- Live attack feed
- MITRE ATT&CK mapping
- Threat actor intelligence

---

# 🛠 Tech Stack

| Technology | Purpose |
|---|---|
| Splunk Enterprise | SIEM Platform |
| Windows Server / Windows 10 | Victim Machine |
| Kali Linux | Attacker Machine |
| Sysmon | Advanced Windows Logging |
| Splunk Universal Forwarder | Log Forwarding |
| XML Dashboard | Splunk Dashboard UI |
| CSS | Custom Dashboard Styling |

---

# 🏗 Lab Architecture

```text
Kali Linux (Attacker)
        │
        ▼
Windows Victim Machine
        │
        ▼
Splunk Universal Forwarder
        │
        ▼
Ubuntu SIEM Server (Splunk Enterprise)
```

---

# 📂 Project Structure

```text
cyber-soc-dashboard/
│
├── README.md
│
├── dashboard/
│   ├── soc_dashboard_v3.xml
│   └── soc_style_2.css
│
├── screenshots/
│   └── dashboard_preview.png
│
└── docs/
    └── setup_guide.md
```

---

# ⚙ Requirements

## Hardware Requirements
- Minimum 8GB RAM
- 50GB Storage
- Intel i5 / Ryzen 5 or higher

## Virtualization Software
Install one of the following:
- VMware Workstation
- VirtualBox

---

# 💻 Operating Systems Used

## Attacker Machine
- Kali Linux

## Victim Machine
- Windows 10 / Windows Server

## SIEM Server
- Ubuntu Server/Desktop

---

# 📥 Dependencies

# Ubuntu SIEM Server

## Install Splunk Enterprise

Download Splunk Enterprise:

https://www.splunk.com/en_us/download/splunk-enterprise.html

Install:

```bash
sudo dpkg -i splunk_package.deb
```

Start Splunk:

```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

Enable boot start:

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

---

# Windows Victim Machine

## Install Sysmon

Download Sysmon:

https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

Install Sysmon:

```powershell
sysmon64.exe -i
```

---

## Install Splunk Universal Forwarder

Download:

https://www.splunk.com/en_us/download/universal-forwarder.html

Configure forwarding to SIEM server.

---

# 🔧 Splunk Configuration

## Step 1 — Login to Splunk

Open browser:

```text
http://YOUR-SIEM-IP:8000
```

---

## Step 2 — Enable Receiving Port

Go to:

```text
Settings → Forwarding and Receiving
```

Add receiving port:

```text
9997
```

---

## Step 3 — Add Data Inputs

Go to:

```text
Settings → Data Inputs
```

Enable:
- WinEventLog
- Sysmon Logs

---

# 📊 Dashboard Installation

## Step 1 — Create Dashboard

Go to:

```text
Dashboards → Create New Dashboard
```

Choose:
- Dashboard Studio or Classic XML Dashboard

---

## Step 2 — Open Edit Source

Inside dashboard:

```text
Edit → Edit Source
```

Delete existing XML code.

Paste contents of:

```text
dashboard/soc_dashboard_v3.xml
```

Save dashboard.

---

# 🎨 CSS Styling Installation

Copy CSS file:

```bash
sudo cp dashboard/soc_style_2.css \
/opt/splunk/etc/apps/search/appserver/static/
```

Restart Splunk:

```bash
sudo /opt/splunk/bin/splunk restart
```

---

# 🚀 Running the Project

## Generate Attack Logs

From Kali Linux:

### Nmap Scan

```bash
nmap TARGET-IP
```

### Hydra RDP Brute Force

```bash
hydra -l administrator -P rockyou.txt rdp://TARGET-IP
```

### SMB Enumeration

```bash
enum4linux TARGET-IP
```

### PowerShell Execution
Run PowerShell commands on Windows machine to generate Sysmon logs.

---

# 📈 Dashboard Panels

## Authentication Monitoring
- Failed Logins
- Successful Logins
- RDP Login Tracking

## Threat Detection
- Brute Force Detection
- Account Lockouts
- Lateral Movement

## Sysmon Monitoring
- PowerShell Execution
- Suspicious Processes
- Credential Access

## Threat Intelligence
- Global Attack Map
- Threat Severity Overview
- MITRE ATT&CK Mapping

---

# 📸 Screenshots

Add screenshots inside:

```text
screenshots/
```

Example:

```markdown
![Dashboard Preview](screenshots/dashboard_preview.png)
```

---

# 🌐 GitHub Upload Steps

## Initialize Git

```bash
git init
```

## Add Files

```bash
git add .
```

## Commit

```bash
git commit -m "Initial commit - Cyber SOC Command Center"
```

## Connect GitHub Repository

```bash
git remote add origin https://github.com/YourUsername/cyber-soc-dashboard.git
```

## Push to GitHub

```bash
git branch -M main
git push -u origin main
```

---

# 🔥 Recommended Improvements

Future enhancements:
- Wazuh Integration
- Sigma Rules
- SOAR Automation
- Email Alerting
- Threat Intelligence APIs
- Malware Sandbox Integration
- AI-based Threat Detection

---

# 🛡 MITRE ATT&CK Techniques Covered

| Technique ID | Description |
|---|---|
| T1110 | Brute Force |
| T1021.001 | RDP |
| T1059 | PowerShell |
| T1003 | Credential Dumping |
| T1550 | Pass-the-Hash |
| T1068 | Privilege Escalation |

---

# ⚠ Disclaimer

This project was developed for educational and defensive cybersecurity purposes in an isolated lab environment.

Do not use these techniques on systems you do not own or have explicit authorization to test.

---

# 👨‍💻 Author

Harish

Cybersecurity Enthusiast | SOC Analyst | Threat Detection | SIEM Monitoring

---

# ⭐ Support

If you found this project useful:
- Star the repository
- Fork the project
- Share with others
- Contribute improvements
