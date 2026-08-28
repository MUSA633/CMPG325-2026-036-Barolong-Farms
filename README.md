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
- [IP Addressing Plan](#-ip-addressing-plan)
- [VLAN Design](#-vlan-design)
- [Wireless Security Implementation](#-wireless-security-implementation)
- [Guest Network Isolation (CR3)](#-guest-network-isolation-cr3)
- [DHCP Configuration](#-dhcp-configuration)
- [Device Configuration Summary](#-device-configuration-summary)
- [Testing and Verification](#-testing-and-verification)
- [Key Design Decisions](#-key-design-decisions)
- [Project Structure](#-project-structure)
- [Commit History](#-commit-history)
- [Future Work](#-future-work-milestone-2)
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
| Distribution Switch | Cisco 2960 (Layer 2) | 1 | Aggregates access switches |
| Access Switches | Cisco 2960 (Layer 2) | N (as needed) | Connects end devices |
| Lightweight Access Points | Cisco AIR-AP1850 | N (as needed) | Wireless coverage |
| Guest Access Point | Cisco WRT300N | 1 | Guest Wi-Fi connectivity |

#### Physical Topology Diagram
