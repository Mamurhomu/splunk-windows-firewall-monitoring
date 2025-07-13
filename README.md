# splunk-windows-firewall-monitoring
# 🛡️ Windows Firewall Monitoring with Splunk | Mini SOC Lab

This project demonstrates a simulated Security Operations Center (SOC) lab using Splunk Enterprise and Universal Forwarders to monitor Windows Firewall activity and system-level logs across multiple virtual machines.

---

## 🔧 Project Overview

### Infrastructure:

- 💻 1 Host Machine with **Splunk Enterprise (Indexer)**
- 🖥️ 3 Windows 11 VMs with **Splunk Universal Forwarder**
- 🔌 Forwarded logs: Security, System, Application, Windows Firewall (pfirewall.log)

### Key Features:<img width="1536" height="1024" alt="ChatGPT Image Jul 13, 2025, 06_58_55 AM" src="https://github.com/user-attachments/assets/0f20725e-e696-4600-9817-74877d78fea7" />
<img width="1920" height="1020" alt="07_Forwarder_Overview_Dashboard" src="https://github.com/user-attachments/assets/38895f9d-360d-4225-9b7d-72467b96e700" />
<img width="1920" height="1020" alt="06_Dashboard_Creation_Steps" src="https://github.com/user-attachments/assets/0abb4d26-535c-4452-adc2-ce7fabced75e" />
<img width="1920" height="1020" alt="04_Receiving_Port_Config" src="https://github.com/user-attachments/assets/f5b2fb24-fb57-40dd-9aa5-31c122712bed" />
<img width="1920" height="1020" alt="03_Universal_Forwarder_Config" src="https://github.com/user-attachments/assets/4fd34be3-9858-47de-a901-a6efa7c5bda8" />
<img width="1920" height="1020" alt="02_Add_Panel_Logs_Dashboard" src="https://github.com/user-attachments/assets/79559c92-6e12-4ca9-97d5-d871d5c1ec97" />
<img width="1920" height="1020" alt="01_Creating_Dashboard" src="https://github.com/user-attachments/assets/16666a04-80c6-4d7f-89f5-cc726480f735" />
<img width="1920" height="1020" alt="01_Creating_Dashboard" src="https://github.com/user-attachments/assets/f103015b-84f8-4b1c-afef-0734a2b25d7c" />


- ✅ Log ingestion via Universal Forwarder → Indexer
- 📡 Port 9997 configured for data reception
- 🧩 Custom dashboards using **Dashboard Studio**
- 🔍 Real-time visibility into:
  - Dropped firewall packets
  - Top source IPs (blocked)
  - Protocols (TCP/UDP/ICMP)
  - Successful logins (4624), privilege use (4672)
  - Unauthorized logins

---

## 📊 Dashboards & Visuals

| Step | Description |
|------|-------------|
| ![Step 1](01_Creating_Dashboard.png) | Creating the base dashboard |
| ![Step 2](02_Add_Panel_Logs_Dashboard.png) | Adding a panel to display host event logs |
| ![Step 3](03_Universal_Forwarder_Config.png) | Configuring and verifying Universal Forwarder |
| ![Step 4](04_Receiving_Port_Config.png) | Port 9997 open and listening on indexer |
| ![Step 5](05_Main_Dashboard_Overview.png) | All panels and layout in Dashboard Studio |
| ![Step 6](06_Dashboard_Creation_Steps.png) | Panel for logon events (SPL query) |
| ![Step 7](07_Forwarder_Overview_Dashboard.png) | Host-level visibility and logs flowing |

---

## 🔍 Sample SPL Queries

**Events by Host:**
```spl
index=* | stats count by host
```

**Successful Login Attempts:**
```spl
index=wineventlog sourcetype="WinEventLog:Security" EventCode=4624
| stats count by host, user, ComputerName
| rename user as "Failed User", host as "Host", ComputerName as "Device Name", count as "Attempts"
| sort -Attempts
```

---

## 🌐 Networking

Each VM's adapter was manually configured in VirtualBox to support bridged/NAT communication. ICMP was enabled for ping visibility across the simulated network.

---

## 🧠 Skills Demonstrated

- SIEM Engineering (Universal Forwarder ➝ Indexer)
- Host-based detection with Windows Defender Firewall
- JSON-based dashboard creation in Splunk Studio
- Network troubleshooting & adapter configuration
- Event parsing, SPL queries, and field extraction
- Hands-on SOC workflows (alert triage, log correlation)

---

📬 **Feel free to fork this repo or reach out if you'd like to build your own mini-SOC setup.**

---

🔖 Tags: `#SOC`, `#SIEM`, `#Splunk`, `#CyberSecurity`, `#HomeLab`, `#WindowsFirewall`, `#DashboardStudio`, `#UniversalForwarder`
