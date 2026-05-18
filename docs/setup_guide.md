# ⚙ Cyber SOC Command Center — Setup Guide

This guide explains how to configure and run the Cyber SOC Command Center in a home lab environment using Splunk SIEM.

---

# 🏗 Lab Setup Overview

## Machines Used

| Machine | Purpose |
|---|---|
| Kali Linux | Attacker Machine |
| Windows 10 / Server | Victim Machine |
| Ubuntu Server/Desktop | SIEM Server |

---

# 🖥 Virtual Machine Setup

## Recommended Specifications

### Ubuntu SIEM Server
- 4 CPU Cores
- 4–8 GB RAM
- 50 GB Storage

### Windows Victim Machine
- 2 CPU Cores
- 4 GB RAM
- 40 GB Storage

### Kali Linux
- 2 CPU Cores
- 2–4 GB RAM
- 30 GB Storage

---

# 🌐 Network Configuration

Set all virtual machines to the same network.

Recommended:
- NAT Network
- Host-Only Adapter
- Bridged Adapter

Verify connectivity:

```bash
ping TARGET-IP
```

---

# 📥 Install Splunk Enterprise

## Ubuntu SIEM Server

Download Splunk Enterprise:

```text
https://www.splunk.com/en_us/download/splunk-enterprise.html
```

Install:

```bash
sudo dpkg -i splunk_package.deb
```

Start Splunk:

```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

Enable startup:

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

Open Splunk:

```text
http://YOUR-SIEM-IP:8000
```

---

# 🔧 Configure Splunk Receiving Port

Go to:

```text
Settings → Forwarding and Receiving
```

Add receiving port:

```text
9997
```

---

# 📥 Install Splunk Universal Forwarder

## Windows Victim Machine

Download:

```text
https://www.splunk.com/en_us/download/universal-forwarder.html
```

Install Splunk Universal Forwarder.

During setup:
- Add SIEM Server IP
- Use port `9997`

Example:

```text
192.168.X.X:9997
```

---

# 📊 Enable Windows Event Logging

Inside Splunk Universal Forwarder:

Enable:
- Security Logs
- System Logs
- Application Logs

---

# 🔍 Install Sysmon

## Windows Machine

Download Sysmon:

```text
https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
```

Extract files.

Install:

```powershell
sysmon64.exe -i
```

Verify Sysmon service:

```powershell
Get-Service Sysmon64
```

---

# 📂 Import Dashboard

## Step 1 — Create Dashboard

Inside Splunk:

```text
Dashboards → Create New Dashboard
```

Choose:
- Classic XML Dashboard

---

## Step 2 — Open Edit Source

Inside dashboard:

```text
Edit → Edit Source
```

Delete default XML.

Open file:

```text
dashboard/soc_dashboard_v3.xml
```

Copy entire XML code and paste it into Splunk.

Click Save.

---

# 🎨 Install Dashboard CSS

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

# 🔄 Update Lab IP Addresses

Open:

```text
dashboard/soc_dashboard_v3.xml
```

Search for:

```text
ATTACK FLOW — Kali Linux to Windows Victim to SIEM
```

Update placeholders:

```xml
ATTACKER-HOST
TARGET-HOST
SIEM-SERVER
```

Replace with your own lab IPs if needed.

Example:

```xml
| eval "Source"="Kali Linux (192.168.X.X)"
| eval "Target"="Windows Victim (192.168.X.X)"
```

---

# 🚀 Generate Test Logs

## Nmap Scan

From Kali Linux:

```bash
nmap TARGET-IP
```

---

## Hydra RDP Brute Force

```bash
hydra -l administrator -P rockyou.txt rdp://TARGET-IP
```

---

## SMB Enumeration

```bash
enum4linux TARGET-IP
```

---

## PowerShell Execution

Run PowerShell commands on Windows machine to generate Sysmon logs.

Example:

```powershell
powershell.exe
```

---

# 📊 Verify Data in Splunk

Run query:

```spl
index=main
```

If logs appear, data forwarding is working correctly.

---

# 🔥 Recommended Enhancements

Future improvements:
- Wazuh Integration
- Sigma Rules
- SOAR Automation
- Threat Intelligence APIs
- Email Alerting
- Malware Sandbox Integration

---

# ⚠ Troubleshooting

## No Logs Appearing

Check:
- Splunk service status
- Universal Forwarder service
- Firewall rules
- Port 9997 connectivity

Test:

```bash
telnet SIEM-IP 9997
```

---

## Dashboard Not Loading

Verify:
- XML pasted correctly
- CSS file copied correctly
- Splunk restarted

---

## Sysmon Logs Missing

Check Sysmon service:

```powershell
Get-Service Sysmon64
```

---

# 🛡 Security Notice

This project is for:
- Educational use
- Home labs
- Defensive cybersecurity learning

Do not perform unauthorized testing on systems you do not own.

---

# 👨‍💻 Author

Your Name

Cybersecurity Enthusiast | SOC Analyst | Threat Detection | SIEM Monitoring
