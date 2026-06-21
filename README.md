# Team 15 Cisco Packet Tracer Network Design

## Overview
This project implements an enterprise network designed in Cisco Packet Tracer using VLAN segmentation, subnetting, and access control policies. The design separates departments, centralizes services, and isolates a DMZ for public-facing systems.

Team Number: 15  
Team Token: I7TWRR  
Base Network: 10.207.0.0/16  

---

## Objectives
- Implement VLAN-based network segmentation
- Design structured subnetting using /24 networks per department
- Enable inter-VLAN routing via gateway interfaces
- Deploy centralized internal services (DNS, Application Server)
- Configure a DMZ for external-facing services
- Enforce traffic control policies between network segments

---

## VLAN Configuration

| VLAN Name        | VLAN ID |
|------------------|--------|
| Sales            | 40     |
| Finance          | 50     |
| Admin            | 60     |
| Guest            | 70     |
| Services         | 80     |
| Branch Staff     | 90     |
| Branch Support   | 100    |
| DMZ              | 110    |

---

## Subnetting and Gateways

| Department       | Subnet            | Gateway        |
|------------------|------------------|---------------|
| Sales            | 10.207.10.0/24   | 10.207.10.1   |
| Finance          | 10.207.20.0/24   | 10.207.20.1   |
| Admin            | 10.207.30.0/24   | 10.207.30.1   |
| Guest            | 10.207.40.0/24   | 10.207.40.1   |
| Services         | 10.207.50.0/24   | 10.207.50.1   |
| Branch Staff     | 10.207.60.0/24   | 10.207.60.1   |
| Branch Support   | 10.207.70.0/24   | 10.207.70.1   |
| DMZ              | 10.207.100.0/24  | 10.207.100.1  |

---

## Key Hosts

| Device               | IP Address       | Function              |
|---------------------|-----------------|----------------------|
| DNS Server          | 10.207.50.10    | Internal DNS         |
| Business App Server | 10.207.50.20    | Internal Application |
| DMZ Web Server      | 10.207.100.10   | Public Web Service   |
| DMZ Mail Server     | 10.207.100.20   | Email Services       |
| Admin Jump Host     | 10.207.30.10    | Secure Admin Access  |

---

## End Device Addressing

| Device            | IP Address       | VLAN | Gateway        |
|------------------|-----------------|------|----------------|
| Sales PC         | 10.207.10.50    | 40   | 10.207.10.1    |
| Finance PC       | 10.207.20.60    | 50   | 10.207.20.1    |
| Admin PC         | 10.207.30.10    | 60   | 10.207.30.1    |
| Guest PC         | 10.207.40.50    | 70   | 10.207.40.1    |
| Services PC      | 10.207.50.10    | 80   | 10.207.50.1    |
| Branch Staff PC  | 10.207.60.10    | 90   | 10.207.60.1    |
| Branch Support   | 10.207.70.50    | 100  | 10.207.70.1    |
| DMZ Hosts        | 10.207.100.10+  | 110  | 10.207.100.1   |

---

## Security Policies

- Sales to Business Application Server: Denied
- Branch Staff to Business Application Server: Allowed
- Administrative access restricted to Admin Jump Host only
- External access restricted to DMZ only
- DMZ cannot initiate connections into internal network

---

## Configuration Summary

- VLANs configured for all departments (40–110)
- Trunk links configured between switches
- Inter-VLAN routing enabled via gateway interfaces
- Internal services hosted on Services VLAN
- DMZ isolated for external-facing services
- ACLs applied for traffic filtering and access control

---

## Testing and Verification

- Intra-VLAN communication: Successful
- Inter-VLAN routing: Verified
- Sales to Application Server: Blocked
- Branch Staff to Application Server: Allowed
- DMZ to internal network initiation: Blocked
- External access to DMZ: Allowed

---

## Repository Structure

team15-network/
├── team15.pkt
├── README.md
├── topology.png
└── configs.txt (optional)

---

## Key Learnings
- VLAN-based enterprise network design
- Structured IP addressing and subnet planning
- Inter-VLAN routing implementation
- DMZ security architecture
- ACL-based traffic control
