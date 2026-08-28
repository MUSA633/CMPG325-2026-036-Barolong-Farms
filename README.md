# Barolong Farms Co-operative Network Design
## CMPG 325 Individual Project - Milestone 1

---

## 📋 Project Overview

| **Item** | **Details** |
|----------|-------------|
| **Project ID** | CMPG325-2026-036 |
| **Client ID** | CLI-036 |
| **Client Name** | Barolong Farms Co-operative (Taung) |
| **Industry** | Agriculture |
| **Assigned Networking Challenge** | Wireless Security (WPA2-PSK Hardening; Enterprise optional extension) |
| **Addressing Block** | 10.19.0.0/16 |
| **Design Constraint** | Seasonal staff double user numbers for three months a year |
| **Change Request (CR3)** | Guest Wi-Fi must be added for visitors, isolated from internal resources |
| **Student Name** | [INSERT YOUR NAME] |
| **Student Number** | [INSERT YOUR STUDENT NUMBER] |
| **Module** | CMPG 325 |
| **Submission Date** | 28 August 2026 |

---

## 📑 Table of Contents

- [Project Description](#-project-description)
- [Client Requirements](#-client-requirements)
- [Physical Topology](#-physical-topology)
- [Logical Topology](#-logical-topology)
- [IP Addressing Plan](#-ip-addressing-plan)
- [VLAN Design](#-vlan-design)
- [Guest Network Isolation (CR3)](#-guest-network-isolation-cr3)
- [Wireless Security Implementation](#-wireless-security-implementation)
- [DHCP Configuration](#-dhcp-configuration)
- [Key Design Decisions](#-key-design-decisions)
- [Project Structure](#-project-structure)
- [Commit History](#-commit-history)
- [Future Work (Milestone 2)](#-future-work-milestone-2)
- [References](#-references)
- [Academic Integrity Statement](#-academic-integrity-statement)

---

## 📖 Project Description

This repository contains the complete network design for **Barolong Farms Co-operative** located in Taung, South Africa. The organization operates in the agricultural industry and requires a robust, scalable network infrastructure that can accommodate seasonal staff increases and provide secure wireless connectivity.

### 🎯 Key Objectives

- ✅ Design and simulate a computer network using Cisco Packet Tracer
- ✅ Implement WPA2-PSK wireless security with hardening measures
- ✅ Create an isolated Guest Wi-Fi network for visitors
- ✅ Accommodate seasonal staff doubling (3 months per year)
- ✅ Provide appropriate connectivity and network services for the agricultural organization
- ✅ Document all design decisions and evidence in GitHub portfolio

---

## 📋 Client Requirements

Based on the project brief for **Barolong Farms Co-operative (Taung)** in the agricultural industry, the following requirements have been identified:

| **Requirement** | **Description** | **Source Reference** |
|-----------------|-----------------|---------------------|
| **Core Connectivity** | Provide appropriate connectivity and network services for the agricultural organization. The completed network must permit successful data exchange between appropriate nodes. | Section 6: Client Requirements |
| **IP Addressing** | Use the assigned addressing block **10.19.0.0/16** as the basis for all IP address allocations throughout the network. | Section 6 & 7 |
| **Wireless Security Challenge** | Implement and demonstrate **Wireless Security (WPA2-PSK hardening)** . Enterprise option is an optional extension. Must configure, verify, and demonstrate this within the assigned client network. | Section 9: Assigned Networking Challenge |
| **Design Constraint - Scalability** | The network must accommodate **seasonal staff doubling user numbers** for three months each year. The design must be scalable to handle this increased load. | Section 8: Design Constraint |
| **Change Request CR3 - Guest Wi-Fi** | **Guest Wi-Fi must be added for visitors**, isolated from internal resources. The final solution must show how the network accommodates this change request. | Section 10: Client Change Request |
| **Packet Tracer Implementation** | Use Cisco Packet Tracer for network implementation and simulation. Design appropriate topology and device arrangement. Configure necessary routers, switches, end devices, and other required nodes. | Section 7: Network Design Requirements |
| **Testing and Verification** | Test relevant end-to-end connectivity. Verify the assigned networking challenge. Capture clear evidence of successful operation/configuration. Document important troubleshooting performed. | Section 11: Testing Requirements |
| **GitHub Portfolio** | Create and maintain an individual GitHub portfolio. Include professional README and appropriate project evidence. Use meaningful commits showing development over time. | Section 12: GitHub Portfolio of Evidence |
| **Video Demonstration** | Submit 15-20 minute individual video with inset webcam view. Introduce yourself, explain client requirements and network design, demonstrate Packet Tracer implementation and assigned networking challenge. | Section 13: Individual Video Demonstration |

---

## 🌐 Physical Topology

### Design Overview

The physical topology follows a **hierarchical three-tier design** (Core-Distribution-Access) to provide scalability, redundancy, and organized network management. This approach is particularly suitable for accommodating the seasonal staff increase, as additional access switches and access points can be added without disrupting the core infrastructure.

### Hardware Components

| **Device Type** | **Model** | **Quantity** | **Purpose** |
|-----------------|-----------|--------------|-------------|
| Core Router | Cisco 4321 | 1 | Gateway for all internal networks, inter-VLAN routing, DHCP services, NAT, and ACL enforcement for guest isolation |
| Core Switch | Cisco 3650 (Layer 3) | 1 | Backbone of the network, provides high-speed switching between distribution layers |
| Wireless LAN Controller (WLC) | Cisco 2500 Series | 1 | Centralized management of all lightweight access points, simplifies configuration and security policy deployment |
| Distribution Switch | Cisco 2960 (Layer 2) | 1 | Aggregates connections from access switches in different buildings/departments |
| Access Switches | Cisco 2960 (Layer 2) | N (as needed) | Connects end devices (administrative PCs, printers, etc.) in various locations across the farm |
| Lightweight Access Points (LAPs) | Cisco AIR-AP1850 | N (as needed) | Provides wireless coverage for staff and seasonal workers across office and farm buildings |
| Guest Access Point / Wireless Router | Cisco WRT300N | 1 | Dedicated or VLAN-separated device providing Guest Wi-Fi connectivity, isolated from internal resources |
| End Devices | Various | N (as needed) | Administrative PCs, staff laptops, smartphones, printers, and visitor devices |

### Physical Topology Diagram

<img width="4111" height="2607" alt="Physical topolgy" src="https://github.com/user-attachments/assets/b62b8e5b-c05d-477d-b8e8-4919ac01378a" />

*Figure 1: Physical Topology Diagram of Barolong Farms Network*

### Physical Layout Description

The network is physically distributed across the farm premises as follows:

**1. Main Building (Administration):**
- Core Router (R1) and Core Switch (S1) are located in a secured server room
- Wireless LAN Controller (WLC) is co-located with core equipment
- Access Switch S3 provides wired connectivity for administrative PCs
- LAP (Office) provides wireless coverage for administrative staff

**2. Farm Operations Area:**
- Distribution Switch (S2) is located in a central equipment room
- Access Switch S4 provides connectivity for operational PCs and printers
- LAP (Farm Buildings) provides wireless coverage for seasonal workers

**3. Visitor Areas:**
- Guest Access Point is strategically placed in reception/visitor areas
- Physical separation is achieved through VLAN isolation on the core router

### Physical Connectivity Summary

| **Connection** | **Media Type** | **Description** |
|----------------|----------------|-----------------|
| Router to Core Switch | Copper (Gigabit Ethernet) | Trunk link carrying all VLANs |
| Core Switch to Distribution Switch | Copper (Gigabit Ethernet) | Trunk link for aggregated traffic |
| Core Switch to WLC | Copper (Fast Ethernet) | Management and control traffic |
| Distribution to Access Switches | Copper (Fast Ethernet) | Access layer connectivity |
| Access Switches to End Devices | Copper (Fast Ethernet) | End-user connectivity |
| WLC to Access Points | Wireless / Copper | CAPWAP protocol for AP management |
| Guest AP to Core Switch | Copper (Fast Ethernet) | Dedicated Guest VLAN connection |

---

## 🔄 Logical Topology

### Design Overview

The logical topology uses **VLAN segmentation** to isolate traffic, improve security, and simplify network management. **Inter-VLAN routing** is performed using a **Router-on-a-Stick** model on the Core Router (R1). **Access Control Lists (ACLs)** are implemented to enforce security policies, particularly for Guest isolation.

### VLAN Design

| **VLAN ID** | **VLAN Name** | **Subnet** | **Description** |
|-------------|---------------|------------|-----------------|
| 10 | Management | 10.19.10.0/24 | Network device management (R1, S1, WLC). Restricted access for authorized administrators only. |
| 20 | Admin Staff | 10.19.20.0/24 | Permanent farm administration staff. Full access to internal servers and resources. |
| 30 | Operations Staff | 10.19.30.0/24 | Seasonal and operational staff in fields/warehouses. Restricted access to specific internal systems. |
| 40 | Internal Wireless | 10.19.40.0/24 | Staff laptops and mobile devices connecting via corporate Wi-Fi. Secured with WPA2-PSK. |
| 99 | Guest Wi-Fi | 10.19.99.0/24 | Visitor internet access. Completely isolated from all internal VLANs via ACL. |

### Subnetting Rationale

The assigned addressing block **10.19.0.0/16** has been subnetted into **/24** networks for the following reasons:

- **Manageability:** /24 subnets provide up to 254 usable hosts, which is sufficient for each VLAN
- **Scalability:** The /24 size allows for easy expansion without complex subnetting changes
- **Broadcast Domain Control:** Smaller subnets limit the size of broadcast domains, improving performance
- **Troubleshooting:** Clear separation of subnets makes problem identification easier
- **Security:** Each VLAN/subnet can have distinct security policies applied

### Logical Topology Diagram

<img width="5904" height="1567" alt="Logical topology" src="https://github.com/user-attachments/assets/4e80fc54-e92e-42b2-8706-70632f02781a" />


---

## 📡 IP Addressing Plan

### VLAN and Subnet Allocation

| **VLAN** | **VLAN Name** | **Network Address** | **Subnet Mask** | **CIDR** | **Usable Host Range** | **Broadcast Address** | **Gateway** |
|----------|---------------|---------------------|-----------------|----------|----------------------|----------------------|-------------|
| 10 | Management | 10.19.10.0 | 255.255.255.0 | /24 | 10.19.10.1 - 10.19.10.254 | 10.19.10.255 | 10.19.10.1 |
| 20 | Admin Staff | 10.19.20.0 | 255.255.255.0 | /24 | 10.19.20.1 - 10.19.20.254 | 10.19.20.255 | 10.19.20.1 |
| 30 | Operations Staff | 10.19.30.0 | 255.255.255.0 | /24 | 10.19.30.1 - 10.19.30.254 | 10.19.30.255 | 10.19.30.1 |
| 40 | Internal Wireless | 10.19.40.0 | 255.255.255.0 | /24 | 10.19.40.1 - 10.19.40.254 | 10.19.40.255 | 10.19.40.1 |
| 99 | Guest Wi-Fi | 10.19.99.0 | 255.255.255.0 | /24 | 10.19.99.1 - 10.19.99.254 | 10.19.99.255 | 10.19.99.1 |

### Device IP Assignments

| **Device** | **Interface** | **IP Address** | **Subnet Mask** | **VLAN** | **Description** |
|------------|---------------|----------------|-----------------|----------|-----------------|
| **Core Router (R1)** | | | | | |
| | GigabitEthernet0/0 | 10.19.254.1 | 255.255.255.0 | - | WAN connection to ISP |
| | GigabitEthernet0/1.10 | 10.19.10.1 | 255.255.255.0 | 10 | Gateway - Management |
| | GigabitEthernet0/1.20 | 10.19.20.1 | 255.255.255.0 | 20 | Gateway - Admin Staff |
| | GigabitEthernet0/1.30 | 10.19.30.1 | 255.255.255.0 | 30 | Gateway - Operations |
| | GigabitEthernet0/1.40 | 10.19.40.1 | 255.255.255.0 | 40 | Gateway - Internal Wireless |
| | GigabitEthernet0/1.99 | 10.19.99.1 | 255.255.255.0 | 99 | Gateway - Guest Wi-Fi |
| **Core Switch (S1)** | | | | | |
| | VLAN 10 SVI | 10.19.10.2 | 255.255.255.0 | 10 | Management interface |
| **Wireless LAN Controller (WLC)** | | | | | |
| | Management Interface | 10.19.10.10 | 255.255.255.0 | 10 | WLC management IP |
| **Lightweight Access Points (LAPs)** | | | | | |
| | Management | DHCP from VLAN 10 | - | 10 | Dynamic IP assignment from DHCP pool |
| **Access Switch S3** | | | | | |
| | VLAN 10 SVI | 10.19.10.11 | 255.255.255.0 | 10 | Management interface |
| **Access Switch S4** | | | | | |
| | VLAN 10 SVI | 10.19.10.12 | 255.255.255.0 | 10 | Management interface |

### Addressing Plan Rationale

| **Design Decision** | **Rationale** |
|---------------------|---------------|
| **/24 Subnets throughout** | Provides up to 254 hosts per VLAN, sufficient for current needs with room for growth. Simplifies management and troubleshooting. |
| **VLAN 10 for Management** | Isolates network device management traffic from user traffic, improving security. |
| **VLAN 40 for Internal Wireless** | Dedicated subnet for wireless staff devices to simplify DHCP management and security policy application. |
| **VLAN 99 for Guest** | Separate subnet with no internal access permissions, directly addressing CR3 requirement. |
| **DHCP for Wireless Clients** | Allows seamless connectivity for seasonal staff without manual IP configuration. |
| **Static IPs for Infrastructure** | Network devices (routers, switches, WLC) have static IPs for reliable management access. |
| **.1 Gateway Convention** | All gateways are .1 on their respective subnets for consistency and ease of troubleshooting. |
| **Shorter Lease for Guest VLAN** | 1-day lease for guests ensures IP addresses are released promptly and pool doesn't exhaust. |

---

## 🚫 Guest Network Isolation (CR3)

### ACL Implementation
