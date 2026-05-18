# ⚡ Cyber SOC Command Center
-Cyber SOC Command Center — A real-time Splunk SIEM dashboard for threat detection, attack monitoring, Windows event analysis, brute-force detection, Sysmon logging, and MITRE ATT&amp;CK visualization in a home SOC lab environment.
-A real-time Security Operations Center (SOC) dashboard built using Splunk SIEM to monitor, detect, and analyze cyber attacks in a home lab environment.

---

# 🛠 Tech Stack

- **SIEM Platform:** Splunk Enterprise
- **Operating Systems:** Kali Linux, Windows, Ubuntu
- **Log Collection:** Splunk Universal Forwarder
- **Security Monitoring:** Windows Event Logs + Sysmon
- **Visualization:** Custom Splunk XML Dashboard + CSS

---

# 🚨 Dashboard Features

- Failed & successful login monitoring
- RDP brute-force attack detection
- Account lockout monitoring
- Privilege escalation detection
- Lateral movement tracking
- PowerShell execution monitoring
- Suspicious process detection
- Pass-the-Hash indicators
- Threat severity visualization
- Global attack map
- MITRE ATT&CK tactic mapping
- Real-time attack event stream

---

# 🏗 SOC Lab Architecture

```text
Kali Linux Attacker
          │
          ▼
Windows Victim Machine
          │
          ▼
Splunk Universal Forwarder
          │
          ▼
Ubuntu Splunk SIEM Server
```

---

# 📂 Project Structure

```text
cyber-soc-dashboard/
│
├── README.md
├── dashboard/
│   ├── soc_dashboard_v3.xml
│   └── soc_style_2.css
├── screenshots/
│   └── dashboard_preview.png
└── docs/
    └── setup_guide.md
```

---

# ⚙ Installation Guide

## 1️⃣ Import Dashboard XML into Splunk

- Open Splunk Web
- Navigate to:

```text
Dashboards → Create New Dashboard
```

- Open the dashboard
- Click:

```text
Edit → Edit Source
```

- Delete existing XML code
- Copy and paste the contents of:

```text
dashboard/soc_dashboard_v3.xml
```

- Click **Save**

---

## 2️⃣ Add Custom CSS Styling

Copy the CSS file to Splunk static assets directory:

```bash
sudo cp dashboard/soc_style_2.css \
/opt/splunk/etc/apps/search/appserver/static/
```

---

## 3️⃣ Restart Splunk

```bash
sudo /opt/splunk/bin/splunk restart
```

---

# 📊 Detection Capabilities

| Detection Type | Event ID |
|---|---|
| Failed Login | 4625 |
| Successful Login | 4624 |
| Account Lockout | 4740 |
| Privilege Escalation | 4672 |
| Explicit Credential Usage | 4648 |
| NTLM Authentication | 4776 |
| Sysmon Process Execution | 1 |

---

# 🧠 MITRE ATT&CK Coverage

- T1110 — Brute Force
- T1021 — Remote Services
- T1059 — PowerShell Execution
- T1003 — Credential Dumping
- T1550 — Pass-the-Hash
- T1068 — Exploitation for Privilege Escalation

---

# 📸 Dashboard Preview

Add screenshots inside:

```text
screenshots/
```

Example:

```markdown
![Dashboard Preview](screenshots/dashboard_preview.png)
```

---

# 🚀 GitHub Deployment

Initialize Git repository:

```bash
git init
git add .
git commit -m "Initial commit - Cyber SOC Command Center"
```

Connect GitHub repository:

```bash
git remote add origin https://github.com/YourUsername/cyber-soc-dashboard.git
git branch -M main
git push -u origin main
```

---

# 🔐 Security Note

This project was built in an isolated lab environment for educational and defensive cybersecurity purposes only.

No public infrastructure or sensitive information is included in this repository.

---

# 👨‍💻 Author

Cybersecurity Enthusiast focused on:
- SOC Operations
- Threat Detection
- SIEM Engineering
- Incident Response
- Threat Hunting
- Windows Security Monitoring
