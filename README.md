# 🔐 Suricata IDS + Nmap Recon Project (VirtualBox Lab)

## 🧠 Overview

This project demonstrates the deployment and testing of the open-source IDS (Intrusion Detection System) **Suricata** on an Ubuntu Server VM, using a Kali Linux VM to simulate potential threats and recon attacks. It showcases real-time detection of network activity and logs captured via Suricata’s built-in rule sets.

## 💻 Lab Setup

### 🖥️ Virtual Machines

| Role          | OS           | Hostname        | IP Address     | Notes                          |
|---------------|--------------|------------------|----------------|--------------------------------|
| IDS Sensor    | Ubuntu 22.04 | klarcsuricata    | 10.x.x.x     | Runs Suricata IDS              |
| Attacker VM   | Kali Linux   | kali             | 10.x.x.x     | Used for Nmap scanning         |

### Network
- VirtualBox Internal Network (`intnet`)
- Static IP addressing on both VMs
- SSH and HTTP ports enabled for scanning/demo

## ⚙️ Tools Used

- **Suricata** (IDS)
- **Nmap** (Port scanning/recon)
- **tail, tcpdump, iptables** for traffic monitoring
- **ET Open Ruleset** for Suricata detection
- **VirtualBox** for virtualization

## 📋 Demonstrated Attacks & Detections

| Action Performed                 | Suricata Detection Example                                 | Priority |
|----------------------------------|-------------------------------------------------------------|----------|
| `sudo apt update` on Ubuntu     | `ET INFO GNU/Linux APT User-Agent`                         | 3        |
| `nmap -sS 10.0.0.183` from Kali | `ET SCAN Possible Nmap User-Agent Observed`               | 1        |
| ICMP echo requests               | `SURICATA ICMPv4 unknown code`                            | 3        |

## 📂 Key Log Sample

```bash
sudo tail -f /var/log/suricata/fast.log
[**] [1:2024364:5] ET SCAN Possible Nmap User-Agent Observed [**] [Classification: Web Application Attack] [Priority: 1] {TCP} 10.0.0.127:63674 -> 10.0.0.183:80
