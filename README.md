# Secure Network Setup with pfSense, Suricata, and DMZ

**Course:** CY3001 - Networks and Cybersecurity-II  
**Semester:** Fall 2024  
**Assignment #4 & #5**  
**Submitted by:** Idrees Khan (22i-1747), Bakhtawar Ilyas (22i-1665)   
 
---

##  Table of Contents

1. [Introduction](#introduction)
2. [Part 1: Network Setup](#part-1-network-setup)
3. [Part 2: pfSense Configuration](#part-2-pfsense-configuration)
4. [Part 3: Suricata Configuration](#part-3-suricata-configuration)
5. [Problems Faced](#problems-faced)

---

##  Introduction

In this assignment, we designed and implemented a secure network infrastructure using **pfSense**, **Suricata**, and a **DMZ**. The goal was to build a layered security architecture separating internal (LAN) and external (WAN/DMZ) resources.

- **pfSense** was used as the main firewall/router, managing WAN, LAN, and DMZ interfaces.
- **Suricata** was configured as an IDS for real-time threat monitoring.
- A web server was deployed in the **DMZ** to safely expose services externally.

---

##  Part 1: Network Setup

###  Tools Used

- **VMware**
- **pfSense VM**
- **Ubuntu VM (LAN client)**
- **Ubuntu VM (DMZ web server)**

###  Network Topology

- **LAN (VMnet11)** - `10.0.0.0/24`
- **DMZ (VMnet13)** - `172.16.0.0/24`
- **WAN (NAT)**

### pfSense Network Interfaces

| Adapter | Interface | Type            |
|---------|-----------|-----------------|
| 1       | WAN       | NAT             |
| 2       | LAN       | Internal (VMnet11) |
| 3       | DMZ       | Internal (VMnet13) |

---

##  Part 2: pfSense Configuration

- Accessed pfSense web interface at `http://10.0.0.253` via LAN.
- Default credentials: `admin` / `pfsense`
- IP Configuration:
  - **LAN**: 10.0.0.253/24
  - **DMZ**: 172.16.0.1/24 (via pfSense)
- Verified ICMP from LAN to firewall (success) and from DMZ (blocked by default).

###  DMZ Web Server Setup

- Installed **nginx** on DMZ Ubuntu VM.
- Verified access via browser through internal network.

---

##  Part 3: Suricata Configuration

- Installed Suricata package via pfSense.
- Applied **ET Open** rules.
- Monitored interfaces: **LAN**, **DMZ**
- Enabled full rule set and generated alerts using:
  ```bash
  sudo nmap -A 172.16.0.10

 ## Firewall Rules
LAN to DMZ
 ICMP & SSH: Allowed
 HTTP (Port 80): Allowed
 All other traffic: Blocked

LAN to WAN
 ICMP & DNS (Port 53): Allowed
 Limited web access via aliases: Google, YouTube, StackOverflow
 All other web traffic: Blocked

WAN to DMZ
 HTTP/HTTPS (80/443): Allowed via NAT
 Direct access to LAN: Blocked

DMZ to WAN
 DNS (53), ICMP, NTP (123): Allowed
 All other outbound traffic: Blocked

❗ Problems Faced
Issue: WAN to DMZ Web Server Inaccessible
Symptom: DMZ web server was unreachable from the WAN side.

Diagnosis:
Port forwarding configured on pfSense.
WAN traffic was redirected to pfSense web GUI instead of the web server.

Verification:
DMZ web server was accessible internally from LAN and DMZ.
Misconfiguration in port forwarding/NAT likely the root cause.
