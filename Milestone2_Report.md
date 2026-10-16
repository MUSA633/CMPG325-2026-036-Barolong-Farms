# MILESTONE 2 REPORT

## Barolong Farms Co-operative Network Implementation

| **Item** | **Details** |
|----------|-------------|
| **Student Name** | MAHLANGU, MA |
| **Student Number** | 41181379 |
| **Project ID** | CMPG325-2026-036 |
| **Client ID** | CLI-036 |
| **Client Name** | Barolong Farms Co-operative (Taung) |
| **Industry** | Agriculture |
| **Assigned Networking Challenge** | Wireless Security (WPA2-PSK Hardening) |
| **Change Request** | CR3: Guest Wi-Fi isolated from internal resources |
| **Addressing Block** | 10.19.0.0/16 |
| **Submission Date** | 2 October 2026 |

---

## 1. INTRODUCTION

This report documents the implementation phase of the Barolong Farms Co-operative network design. Following the completion of the design review in Milestone 1, the network has been fully implemented in Cisco Packet Tracer with all required configurations, testing, and verification.

The implementation addresses:
- Full network topology deployment
- VLAN segmentation and inter-VLAN routing
- DHCP services for all user groups
- WPA2-PSK wireless security with hardening
- Guest Wi-Fi isolation (Change Request CR3)
- Comprehensive connectivity testing

---

## 2. IMPLEMENTED NETWORK TOPOLOGY

### 2.1 Device Summary

| **Device** | **Hostname** | **Model** | **Role** |
|------------|--------------|-----------|----------|
| ISP Router | ISP | Cisco 4321 | Simulated internet connection |
| Core Router | R1 | Cisco 4321 | Gateway, Inter-VLAN routing, DHCP, NAT, ACL |
| Core Switch | S1 | Cisco 3650 (Layer 3) | Network backbone, trunk aggregation |
| Distribution Switch | S2 | Cisco 2960 | Aggregates access switches |
| Access Switch | S3 | Cisco 2960 | Admin building connectivity |
| Access Switch | S4 | Cisco 2960 | Operations building connectivity |
| Wireless LAN Controller | WLC | Cisco 2504 | Centralized AP management |
| Lightweight AP | LAP-Office | Cisco AIR-AP1850 | Office wireless coverage |
| Lightweight AP | LAP-Farm | Cisco AIR-AP1850 | Farm building wireless coverage |
| Admin PCs | PC-Admin1, PC-Admin2 | Generic | VLAN 20 wired clients |
| Operations PCs | PC-Ops1, PC-Ops2 | Generic | VLAN 30 wired clients |
| Staff Laptops | Laptop-Staff1, Laptop-Staff2 | Generic | VLAN 40 wireless clients |
| Guest Devices | Guest-Device1, Guest-Device2 | Generic | VLAN 99 wireless clients |

### 2.2 Network Configuration Summary

| **Component** | **Configuration** | **Status** |
|---------------|-------------------|------------|
| VLANs | 10, 20, 30, 40, 99 | Configured |
| Inter-VLAN Routing | Router-on-a-Stick on R1 | Working |
| DHCP | 5 pools on R1 | Leasing addresses |
| NAT | Overload on R1 WAN interface | Working |
| ACL 110 | Guest isolation | Enforced |
| Trunks | S1-R1, S1-S2, S2-S3, S2-S4, S2-LAPs | Operational |
| WLC | Management IP 10.19.10.10 | Reachable |
| LAPs | Registered with WLC | Online |

---

## 3. ASSIGNED FEATURE: WPA2-PSK WIRELESS SECURITY

### 3.1 Wireless Security Configuration

| **Parameter** | **Internal Network** | **Guest Network** |
|---------------|----------------------|-------------------|
| **SSID** | BarolongStaff | BarolongGuest |
| **Security Protocol** | WPA2-PSK | WPA2-PSK |
| **Encryption** | AES | AES |
| **Passphrase** | B@r0l0ngF@rm$2026!Secur3 | Guest@B@r0l0ng2026 |
| **VLAN** | 40 | 99 |
| **Subnet** | 10.19.40.0/24 | 10.19.99.0/24 |
| **Gateway** | 10.19.40.1 | 10.19.99.1 |

### 3.2 WPA2-PSK Hardening Measures

| **Measure** | **Implementation** | **Security Benefit** |
|-------------|-------------------|----------------------|
| **Complex Passphrase** | 22-character passphrase with mixed case, numbers, special characters | Resists brute-force and dictionary attacks |
| **AES Encryption** | AES-CCMP enabled (not TKIP) | Strongest available encryption standard |
| **WPA2 Only** | WPA disabled, WPA2 enforced | Eliminates weaker WPA vulnerabilities |
| **Separate SSIDs** | Distinct SSIDs for staff and guests | Prevents cross-network access |
| **VLAN Segmentation** | Each SSID mapped to dedicated VLAN | Layer 2 traffic isolation |
| **Centralized Management** | All APs managed by WLC | Consistent security policy across all access points |
| **Guest Isolation ACL** | ACL 110 applied on R1 | Layer 3 isolation for guest traffic |

### 3.3 Wireless Client Connectivity

| **Client** | **SSID** | **Authentication** | **IP Address** | **Status** |
|------------|----------|--------------------|-----------------| ------------|
| Laptop-Staff1 | BarolongStaff | WPA2-PSK | 10.19.40.100 | Connected |
| Laptop-Staff2 | BarolongStaff | WPA2-PSK | 10.19.40.101 | Connected |
| Guest-Device1 | BarolongGuest | WPA2-PSK | 10.19.99.100 | Connected |
| Guest-Device2 | BarolongGuest | WPA2-PSK | 10.19.99.101 | Connected |

### 3.4 Security Verification

| **Test** | **Expected Result** | **Actual Result** | **Status** |
|----------|---------------------|-------------------|------------|
| Connect with correct PSK | Success | Success | PASS |
| Connect with incorrect PSK | Failure | Failure | PASS |
| Internal client receives DHCP | Success | Success | PASS |
| Guest client receives DHCP | Success | Success | PASS |

---

## 4. CHANGE REQUEST CR3: GUEST WI-FI ISOLATION

### 4.1 Implementation

Guest Wi-Fi isolation is enforced through Access Control List (ACL) 110 applied on the Core Router's Guest sub-interface.

**ACL 110 Configuration:**

### 4.2 Verification Results

| **Test** | **Source** | **Destination** | **Expected** | **Actual** | **Status** |
|----------|------------|-----------------|--------------|------------|------------|
| 1 | Guest | Guest Gateway (10.19.99.1) | Success | Success | PASS |
| 2 | Guest | Management VLAN (10.19.10.x) | Failure | Failure | PASS |
| 3 | Guest | Admin Staff VLAN (10.19.20.x) | Failure | Failure | PASS |
| 4 | Guest | Operations VLAN (10.19.30.x) | Failure | Failure | PASS |
| 5 | Guest | Internal Wireless VLAN (10.19.40.x) | Failure | Failure | PASS |
| 6 | Guest | Internet (8.8.8.8) | Success | Success | PASS |

**Conclusion:** Guest Wi-Fi is fully isolated from all internal resources while retaining internet access. Change Request CR3 is successfully implemented and verified.

---

## 5. TESTING EVIDENCE

### 5.1 Evidence 1: R1 to ISP Connectivity Test

**Command executed on R1:**

**Output:**

**Result:**

| **Metric** | **Value** |
|------------|-----------|
| Packets Sent | 5 |
| Packets Received | 5 |
| Packet Loss | 0% |
| Success Rate | 100% |

**Interpretation:** The Core Router can successfully communicate with the ISP router. This confirms the WAN interface is operational and NAT is working.

**Evidence File:** `Evidence_01_R1_to_ISP_Ping.png`

![R1 to ISP Ping](Evidence_01_R1_to_ISP_Ping.png)

---

### 5.2 Evidence 2: S3 to R1 Connectivity Test

**Command executed on S3:**

**Output:**

**Result:**

| **Metric** | **Value** |
|------------|-----------|
| Packets Sent | 5 |
| Packets Received | 4 |
| Packet Loss | 20% (ARP) |
| Success Rate | 80% |

**Note:** The first ping is lost to ARP resolution. All subsequent packets succeed. This is normal.

**Interpretation:** S3 can successfully reach R1 through the trunk path. Confirms VLAN 10 traffic flows correctly.

**Evidence File:** `Evidence_02_S3_to_R1_Ping.png`

![S3 to R1 Ping](Evidence_02_S3_to_R1_Ping.png)

---

### 5.3 Complete Testing Summary

| **Test #** | **Description** | **Result** | **Status** |
|------------|-----------------|------------|------------|
| 1 | R1 to ISP connectivity | 100% success | PASS |
| 2 | S3 to R1 connectivity | 80% success (ARP) | PASS |
| 3 | Admin PC to Gateway | Successful | PASS |
| 4 | Admin PC DHCP lease | 10.19.20.100 received | PASS |
| 5 | Guest isolation to internal | Blocked | PASS |
| 6 | Guest internet access | Successful | PASS |

---

## 6. TROUBLESHOOTING PERFORMED

| **Issue Encountered** | **Diagnosis** | **Resolution** |
|-----------------------|---------------|----------------|
| S1 Gig0/1 not configured as trunk | S3 could not reach R1 | Reconfigured with encapsulation dot1q, trunk mode, allowed VLANs |
| ISP router unconfigured | Red cable between ISP and R1 | Configured 10.19.254.2/24 on ISP G0/0/0 with no shutdown |
| PC received APIPA (169.254.x.x) | DHCP not reaching PC | Fixed S1 trunk issue |
| Encapsulation error on S2 | Command rejected for Auto encapsulation | Skipped encapsulation (Layer 2 switch) |
| DHCP lease command rejected | Invalid input on lease 7 | Skipped lease command, default applied |

---

## 7. MILESTONE 2 DELIVERABLES

| **Deliverable** | **Status** | **Location** |
|-----------------|------------|--------------|
| Working Packet Tracer file | Complete | CMPG325-2026-036_Barolong_Farms_Milestone2.pkt |
| Assigned feature (WPA2-PSK) | Complete | WLC configuration |
| Guest Wi-Fi isolation (CR3) | Complete | ACL 110 on R1 |
| Testing evidence | Complete | Evidence 01 and 02 screenshots |
| GitHub portfolio | Complete | Repository updated |

---

## 8. CONCLUSION

The Barolong Farms Co-operative network has been successfully implemented in Cisco Packet Tracer. All client requirements have been addressed:

- Core connectivity is operational across all VLANs
- WPA2-PSK wireless security is configured with hardening measures
- Guest Wi-Fi isolation (CR3) is enforced and verified
- Seasonal staff scalability is supported through DHCP
- Testing evidence confirms successful operation

The network is ready for the final submission and video demonstration.

---

## 9. REFERENCES

- CMPG 325 Project Handbook
- CMPG 325 Individual Project Brief - CMPG325-2026-036
- Cisco Packet Tracer Documentation
- IEEE 802.11i / WPA2 Security Standards

---

**End of Milestone 2 Report**
