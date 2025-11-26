# Snort IDS on Kali Linux for Reconnaissance Detection

This project sets up Snort v3 on Kali Linux as an Intrusion Detection System (IDS) to detect early-stage reconnaissance such as ICMP ping sweeps, Nmap TCP SYN scans, and XMAS scans inside a VMware virtual lab. A Windows 11 attacker machine generates traffic, and Snort on Kali logs and classifies the alerts.

## 1. Lab Overview

- **Victim / IDS**: Kali Linux running Snort v3
- **Attacker**: Windows 11
- **Virtualization**: VMware virtual network
- **Monitored network**: `192.168.0.0/16` (border network in Snort rules)
- **Traffic types**:
  - ICMP ping sweeps
  - Nmap host discovery (`-sn`)
  - Nmap TCP port scans (`-sT`)
  - Nmap XMAS tree scans

The goal is to detect reconnaissance attempts and analyze true positives vs false positives in Snort alerts.

## 2. Objectives

- Install and configure Snort on Kali Linux as an IDS.
- Create custom Snort rules for:
  - ICMP echo requests / ping scans
  - Nmap TCP SYN scans on ports 22, 80, 443
  - Nmap XMAS tree scans
- Generate attack traffic from a Windows host.
- Capture and analyze Snort alerts, including:
  - True positives (actual recon)
  - False positives (benign but matching rules)

## 3. Repository Contents

- `docs/Part-3-Snort-IDS-Setup-and-Alert-Analysis.docx`  
  Full lab report with screenshots and detailed discussion.

- `config/snort.lua`  
  Snort configuration file used in the lab.

- `rules/local.rules`  
  Custom Snort rules used to detect ICMP and Nmap scans.

- `logs/sample-alert_fast.txt`  
  Sample `alert_fast` output from Snort during the experiment.

## 4. Environment & Requirements

- **OS (IDS)**: Kali Linux
- **OS (Attacker)**: Windows 11
- **Hypervisor**: VMware (any edition supporting virtual networking)
- **Snort**: Snort v3 (from Kali repos)
- **Tools on attacker**:
  - `ping`
  - `nmap`

## 5. Installing Snort on Kali

From Kali:

```bash
sudo apt-get update
sudo apt-get install snort
