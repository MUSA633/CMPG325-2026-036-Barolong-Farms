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
- [Network Design](#-network-design)
  - [Physical Topology](#physical-topology)
  - [Logical Topology](#logical-topology)
  - [IP Addressing Plan](#ip-addressing-plan)
- [VLAN Design](#-vlan-design)
- [Wireless Security Implementation](#-wireless-security-implementation)
- [Guest Network Isolation (CR3)](#-guest-network-isolation-cr3)
- [DHCP Configuration](#-dhcp-configuration)
- [Device Configuration Summary](#-device-configuration-summary)
- [Testing and Verification](#-testing-and-verification)
- [Key Design Decisions](#-key-design-decisions)
- [Project Structure](#-project-structure)
- [Commit History](#-commit-history)
- [Future Work (Milestone 2)](#-future-work-milestone-2)
- [References](#-references)
- [Academic Integrity Statement](#-academic-integrity-statement)

---

## 📖 Project Description

This repository contains the complete network design and implementation for **Barolong Farms Co-operative** located in Taung, South Africa. The organization operates in the agricultural industry and requires a robust, scalable network infrastructure that can accommodate seasonal staff increases and provide secure wireless connectivity.

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

| **Requirement** | **Description** | **Source** |
|-----------------|-----------------|------------|
| **Core Connectivity** | Provide appropriate connectivity and network services for the agricultural organization | Section 6 |
| **IP Addressing** | Use assigned addressing block 10.19.0.0/16 | Section 6 & 7 |
| **Wireless Security** | Implement and demonstrate WPA2-PSK hardening | Section 9 |
| **Scalability** | Accommodate seasonal staff doubling user numbers for three months annually | Section 8 |
| **Guest Wi-Fi (CR3)** | Add Guest Wi-Fi for visitors, isolated from internal resources | Section 10 |
| **Packet Tracer** | Use Cisco Packet Tracer for implementation and simulation | Section 7 |
| **Testing** | Demonstrate successful connectivity and testing | Section 11 |
| **Documentation** | Maintain GitHub portfolio with professional README and evidence | Section 12 |
| **Video Demonstration** | Submit 15-20 minute video with webcam view | Section 13 |

---

## 🌐 Network Design

### Physical Topology

The network follows a **hierarchical three-tier design** (Core-Distribution-Access) to provide scalability, redundancy, and organized network management. This approach is particularly suitable for accommodating the seasonal staff increase.

#### Hardware Components

| **Device Type** | **Model** | **Quantity** | **Purpose** |
|-----------------|-----------|--------------|-------------|
| Core Router | Cisco 4321 | 1 | Gateway, inter-VLAN routing, DHCP, NAT, ACL |
| Core Switch | Cisco 3650 (Layer 3) | 1 | Backbone of the network |
| Wireless LAN Controller | Cisco 2500 Series | 1 | Centralized AP management |
| Distribution S
---

## 📡 IP Addressing Plan

### VLAN and Subnet Allocation

| **VLAN** | **VLAN Name** | **Network Address** | **CIDR** | **Usable Range** | **Gateway** | **Hosts** |
|----------|---------------|---------------------|----------|------------------|-------------|-----------|
| 10 | Management | 10.19.10.0 | /24 | 10.19.10.1 - 10.19.10.254 | 10.19.10.1 | 254 |
| 20 | Admin Staff | 10.19.20.0 | /24 | 10.19.20.1 - 10.19.20.254 | 10.19.20.1 | 254 |
| 30 | Operations Staff | 10.19.30.0 | /24 | 10.19.30.1 - 10.19.30.254 | 10.19.30.1 | 254 |
| 40 | Internal Wireless | 10.19.40.0 | /24 | 10.19.40.1 - 10.19.40.254 | 10.19.40.1 | 254 |
| 99 | Guest Wi-Fi | 10.19.99.0 | /24 | 10.19.99.1 - 10.19.99.254 | 10.19.99.1 | 254 |

### Device IP Assignments

| **Device** | **Interface** | **IP Address** | **Subnet** | **VLAN** | **Description** |
|------------|---------------|----------------|------------|----------|-----------------|
| **Core Router (R1)** | | | | | |
| | GigabitEthernet0/0 | 10.19.254.1 | /24 | - | WAN to ISP |
| | GigabitEthernet0/1.10 | 10.19.10.1 | /24 | 10 | Gateway - Management |
| | GigabitEthernet0/1.20 | 10.19.20.1 | /24 | 20 | Gateway - Admin Staff |
| | GigabitEthernet0/1.30 | 10.19.30.1 | /24 | 30 | Gateway - Operations |
| | GigabitEthernet0/1.40 | 10.19.40.1 | /24 | 40 | Gateway - Internal Wireless |
| | GigabitEthernet0/1.99 | 10.19.99.1 | /24 | 99 | Gateway - Guest Wi-Fi |
| **Core Switch (S1)** | | | | | |
| | VLAN 10 SVI | 10.19.10.2 | /24 | 10 | Management |
| **WLC** | | | | | |
| | Management | 10.19.10.10 | /24 | 10 | WLC Management |
| **Access Switch S3** | | | | | |
| | VLAN 10 SVI | 10.19.10.11 | /24 | 10 | Management |
| **Access Switch S4** | | | | | |
| | VLAN 10 SVI | 10.19.10.12 | /24 | 10 | Management |
| **LAPs** | | | | | |
| | Management | DHCP from VLAN 10 | - | 10 | Dynamic IP |

---

## 🏗️ VLAN Design

### VLAN Configuration Summary
witch | Cisco 2960 (Layer 2) | 1 | Aggregates access switches |
| Access Switches | Cisco 2960 (Layer 2) | N (as needed) | Connects end devices |
| Lightweight Access Points | Cisco AIR-AP1850 | N (as needed) | Wireless coverage |
| Guest Access Point | Cisco WRT300N | 1 | Guest Wi-Fi connectivity |

#### Physical Topology Diagram

---

## 🔐 Wireless Security Implementation

### WPA2-PSK Configuration

| **Parameter** | **Configuration** |
|---------------|-------------------|
| **Security Protocol** | WPA2-PSK |
| **Encryption** | AES (Advanced Encryption Standard) |
| **Internal SSID** | BarolongStaff |
| **Guest SSID** | BarolongGuest |
| **Internal PSK** | B@r0l0ngF@rm$2026!Secur3 |
| **Guest PSK** | Guest@B@r0l0ng2026 |

### Hardening Measures Implemented

| **Measure** | **Description** |
|-------------|-----------------|
| ✅ **Complex Passphrase** | Non-dictionary, mixed case, numbers, and special characters |
| ✅ **AES Encryption** | Instead of weaker TKIP |
| ✅ **Separate SSIDs** | Internal and Guest networks have different SSIDs |
| ✅ **VLAN Segmentation** | Each SSID assigned to different VLAN |
| ✅ **WLC Management** | Centralized control over all APs |
| ✅ **Guest Isolation** | ACL blocks Guest access to internal resources |

---

## 🚫 Guest Network Isolation (CR3)

### ACL Implementation

To satisfy Change Request CR3, an Access Control List (ACL) is applied on the Core Router to block Guest VLAN 99 from accessing internal networks:

```cisco
! ================================================================
! ACL 110 - Applied to VLAN 99 Gateway Interface (inbound)
! Purpose: Isolate Guest Wi-Fi from all internal networks
! ================================================================

! Deny Guest VLAN to Management VLAN
access-list 110 deny ip 10.19.99.0 0.0.0.255 10.19.10.0 0.0.0.255

! Deny Guest VLAN to Admin Staff VLAN
access-list 110 deny ip 10.19.99.0 0.0.0.255 10.19.20.0 0.0.0.255

! Deny Guest VLAN to Operations Staff VLAN
access-list 110 deny ip 10.19.99.0 0.0.0.255 10.19.30.0 0.0.0.255

! Deny Guest VLAN to Internal Wireless VLAN
access-list 110 deny ip 10.19.99.0 0.0.0.255 10.19.40.0 0.0.0.255

! Permit all other traffic (Internet, DHCP, DNS)
access-list 110 permit ip any any

! ================================================================
! Apply ACL to Guest sub-interface
! ================================================================

interface GigabitEthernet0/1.99
 encapsulation dot1Q 99
 ip address 10.19.99.1 255.255.255.0
 ip access-group 110 in
