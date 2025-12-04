# High Availability Enterprise Network Design (Cisco CML)

![Topology Diagram](images/topology_diagram.png)

## 📌 Project Overview
This project demonstrates a robust, fault-tolerant Campus Network architecture designed for high availability and security. The simulation was built using **Cisco Modeling Labs (CML)** using IOSv and IOSvL2 images.

The primary goal was to design a network that eliminates Single Points of Failure (SPOF) at layers 2 and 3, while securing the access layer against common LAN attacks.

## 🛠️ Key Technologies & Features

### Core & Distribution Layer (Layer 3)
* **OSPF Area 0:** Dynamic routing between Core (C1) and Distribution (D1/D2) layers using `dot1q` subinterfaces.
* **HSRPv2 (Hot Standby Router Protocol):** Gateway redundancy for end-users with sub-second failover.
* **Load Balancing:** Active/Active traffic distribution using HSRP groups and OSPF ECMP.

### Distribution & Access Layer (Layer 2)
* **MSTP (Multiple Spanning Tree Protocol):** Utilized to load-balance VLAN traffic across redundant links (Instance 1 Root: D1, Instance 2 Root: D2).
* **VLAN Segmentation:** Traffic separation for different user groups (VLANs 10, 20, 30, 40).
* **DHCP Split-Scope:** Redundant DHCP services provided by Distribution switches.

### 🛡️ Security Implementation (The "Fortress" Approach)
* **DHCP Snooping:** Prevents Rogue DHCP servers from disrupting the network.
* **Dynamic ARP Inspection (DAI):** Mitigates ARP Spoofing/Man-in-the-Middle attacks.
* **Port Security (Sticky MAC):** Restricts physical access ports to specific devices to prevent unauthorized access.

## 📂 Project Structure

- `configs/` - Contains the final running-configuration for all devices.
    - `C1_Core.cfg` - Core Router configuration.
    - `D1_Distribution.cfg` & `D2_Distribution.cfg` - Distribution Layer Switches.
    - `A1_Access.cfg` & `A2_Access.cfg` - Access Layer Switches with security features.
- `images/` - Network topology diagrams.

## 🚀 Simulation Details
* **Platform:** Cisco CML
* **Nodes:** 1 Core Router, 2 Distro Switches, 2 Access Switches, 4 Alpine Linux Hosts.
* **Verification:** All hosts successfully obtained IP addresses via DHCP and achieved full connectivity (inter-VLAN routing) with redundancy testing.

---
*Created by Mateusz W.*
