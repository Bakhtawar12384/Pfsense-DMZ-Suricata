# Pfsense-DMZ-Suricata
# Secure Network Setup with pfSense, Suricata, and DMZ

## Introduction
This project focuses on designing and implementing a secure network infrastructure using **pfSense**, **Suricata**, and a **DMZ (Demilitarized Zone)**. The goal is to separate internal and external resources while safeguarding critical assets. 

- **pfSense** is configured as the primary firewall, managing traffic across three network zones: WAN, LAN, and DMZ.
- **Suricata** serves as an Intrusion Detection System (IDS), monitoring network traffic for potential threats.
- A **DMZ** hosts a web server on an isolated subnet, providing a security layer for external-facing services.

By implementing proper IP addressing, firewall rules, and routing configurations, we aim to create a robust and secure network environment.

---

## Tech Stack
The following tools and technologies are used in this project:

1. **VMware** – For creating and managing virtual machines.
2. **pfSense VM** – Acts as the firewall and network gateway. (Download from [official site](https://www.pfsense.org) or [Internet Archive](https://archive.org))
3. **Ubuntu VM** – Used as a client machine in the internal LAN.
4. **Ubuntu VM (Web Server)** – Hosts a web service using **Nginx** in the DMZ.

---

## Network Topology
The network is structured as follows:

- **Internal LAN**: Contains a client machine.
- **DMZ**: Hosts a web server running **Nginx**.
- **pfSense Firewall**: Configured with three interfaces:
  - **WAN** – Connects to the external network (Internet).
  - **LAN** – Connects to the internal network (trusted zone).
  - **DMZ** – Hosts externally accessible services in a controlled environment.

---

## Installation & Configuration

### Step 1: Setting Up Virtual Machines
1. Install **VMware Workstation/VirtualBox**.
2. Download and install **pfSense**.
3. Create two Ubuntu VMs:
   - One for the **internal LAN** (client machine).
   - One for the **DMZ web server**.

### Step 2: Configuring pfSense Firewall
1. Assign **WAN, LAN, and DMZ** interfaces.
2. Set up **firewall rules** to control traffic between the network zones.
3. Configure **NAT (Network Address Translation)** for external access to the DMZ.

### Step 3: Deploying the Web Server in DMZ
1. Install **Nginx** on the Ubuntu VM in the DMZ:
   sudo apt update && sudo apt install nginx -y
Adjust firewall rules in pfSense to allow external HTTP/S traffic.

###Step 4: Implementing Suricata IDS
Install Suricata on pfSense via package manager.
Enable Intrusion Detection Mode and configure rule sets.
Monitor and analyze traffic logs for potential threats.

Security Enhancements:
Strict firewall rules: Limiting access between LAN, DMZ, and WAN.
Intrusion Detection System (Suricata): Alerts and blocks malicious activities.
DMZ Segmentation: Reduces attack surface by isolating the web server from the internal network.

Conclusion
This setup demonstrates how pfSense, Suricata, and a DMZ can work together to create a secure network architecture. By effectively segmenting network zones and implementing security controls, we achieve enhanced protection for internal and external resources.
