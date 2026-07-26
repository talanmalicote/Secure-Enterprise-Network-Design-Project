# Team 15 — Cisco Packet Tracer Enterprise Network Design

**Team Number:** 15
**Team Token:** I7TWRR
**Base Network:** 10.207.0.0/16
**Course:** CYB 235, Miami University — Spring 2026

## Short Intro

This project is a secure, multi-site enterprise network built in Cisco Packet Tracer. As Project Lead, I directed a team through the design and implementation of a network spanning a headquarters site, a branch site, and a DMZ. The goal was to take a single /16 address block and turn it into a segmented, policy-enforced network that mirrors how a real organization separates departments, centralizes shared services, and isolates anything exposed to the outside world. The design uses VLAN segmentation, structured subnetting, inter-VLAN routing, and access control lists (ACLs) to enforce a least-privilege traffic model — departments can only reach what they're supposed to reach, and the DMZ can be reached from outside but can never reach back into the internal network.

## Technologies

- **Cisco Packet Tracer** 
- **VLANs (802.1Q)** 
- **Inter-VLAN Routing** 
- **Subnetting (VLSM)** 
- **Access Control Lists (ACLs)** 
- **NAT/PAT and Static Routing** 
- **DNS**

## Features

- **8 VLANs** covering Sales, Finance, Admin, Guest, Services, Branch Staff, Branch Support, and DMZ
- **Structured /24 subnetting** for every department, cleanly carved out of the 10.207.0.0/16 base network
- **Centralized internal services** — a DNS server and business application server hosted on a dedicated Services VLAN
- **Isolated DMZ** hosting a public web server and mail server, reachable from outside but walled off from internal VLANs
- **Inter-VLAN routing** via gateway interfaces so departments can communicate where policy allows
- **Enforced security policies**, including:
  - Sales denied access to the Business Application Server
  - Branch Staff allowed access to the Business Application Server
  - Administrative access restricted to a dedicated Admin Jump Host
  - External access restricted to the DMZ only
  - DMZ blocked from initiating connections into the internal network

### VLAN Configuration

| VLAN Name | VLAN ID |
|---|---|
| Sales | 40 |
| Finance | 50 |
| Admin | 60 |
| Guest | 70 |
| Services | 80 |
| Branch Staff | 90 |
| Branch Support | 100 |
| DMZ | 110 |

### Subnetting and Gateways

| Department | Subnet | Gateway |
|---|---|---|
| Sales | 10.207.10.0/24 | 10.207.10.1 |
| Finance | 10.207.20.0/24 | 10.207.20.1 |
| Admin | 10.207.30.0/24 | 10.207.30.1 |
| Guest | 10.207.40.0/24 | 10.207.40.1 |
| Services | 10.207.50.0/24 | 10.207.50.1 |
| Branch Staff | 10.207.60.0/24 | 10.207.60.1 |
| Branch Support | 10.207.70.0/24 | 10.207.70.1 |
| DMZ | 10.207.100.0/24 | 10.207.100.1 |

### Key Hosts

| Device | IP Address | Function |
|---|---|---|
| DNS Server | 10.207.50.10 | Internal DNS |
| Business App Server | 10.207.50.20 | Internal Application |
| DMZ Web Server | 10.207.100.10 | Public Web Service |
| DMZ Mail Server | 10.207.100.20 | Email Services |
| Admin Jump Host | 10.207.30.10 | Secure Admin Access |

### End Device Addressing

| Device | IP Address | VLAN | Gateway |
|---|---|---|---|
| Sales PC | 10.207.10.50 | 40 | 10.207.10.1 |
| Finance PC | 10.207.20.60 | 50 | 10.207.20.1 |
| Admin PC | 10.207.30.10 | 60 | 10.207.30.1 |
| Guest PC | 10.207.40.50 | 70 | 10.207.40.1 |
| Services PC | 10.207.50.10 | 80 | 10.207.50.1 |
| Branch Staff PC | 10.207.60.10 | 90 | 10.207.60.1 |
| Branch Support | 10.207.70.50 | 100 | 10.207.70.1 |
| DMZ Hosts | 10.207.100.10+ | 110 | 10.207.100.1 |

### Security Policies

- Sales → Business Application Server: **Denied**
- Branch Staff → Business Application Server: **Allowed**
- Administrative access restricted to the Admin Jump Host only
- External access restricted to the DMZ only
- DMZ cannot initiate connections into the internal network

## The Process

1. **Planning the address space** — Started from the assigned base network, 10.207.0.0/16, and broke it into /24 subnets so every department, service group, and the DMZ each got its own clean block with room to grow.
2. **Designing the VLAN structure** — Mapped departments and functions to VLAN IDs (40–110), separating end-user segments (Sales, Finance, Admin, Guest, Branch Staff, Branch Support) from shared infrastructure (Services) and public-facing systems (DMZ).
3. **Building the topology in Packet Tracer** — Laid out switches, routers, and end devices for the HQ site, branch site, and DMZ, then configured trunk links between switches to carry all VLAN traffic.
4. **Configuring inter-VLAN routing** — Set up gateway interfaces (router-on-a-stick / SVIs) so traffic could route between VLANs where policy allowed it.
5. **Deploying centralized services** — Hosted the DNS server and business application server on the Services VLAN so every department could resolve names and reach shared applications through a single, controlled path.
6. **Hardening the DMZ** — Isolated the DMZ VLAN so the public web and mail servers could be reached from outside, without any path back into the internal network.
7. **Writing and applying ACLs** — Implemented access control lists to enforce least-privilege traffic flow, including the Sales-vs-Branch-Staff access differences and the Admin Jump Host restriction.
8. **Testing and verification** — Systematically tested intra-VLAN, inter-VLAN, and DMZ traffic paths to confirm the policies behaved exactly as designed (see results below).

### Testing and Verification Results

| Test | Result |
|---|---|
| Intra-VLAN communication | Successful |
| Inter-VLAN routing | Verified |
| Sales → Application Server | Blocked |
| Branch Staff → Application Server | Allowed |
| DMZ → internal network initiation | Blocked |
| External access → DMZ | Allowed |

## What I Learned

- How to translate a single large address block into a structured, department-based subnetting scheme using VLSM
- Practical implementation of VLAN-based segmentation and how it maps to real organizational boundaries
- How inter-VLAN routing actually moves traffic between segments, and where that traffic needs to be filtered rather than freely allowed
- How to design and apply ACLs to enforce a least-privilege model instead of a flat, fully-open network
- Why centralizing services (DNS, applications) on their own VLAN simplifies both access control and troubleshooting
- How a DMZ is architected so it's reachable from outside but can never be used as a launch point into internal systems
- Coordinating a team through a multi-stage design project — dividing addressing, topology, and policy work while keeping the overall design consistent

## What Could Be Improved

- Add **redundant links and routing** (e.g., HSRP/VRRP, EtherChannel) so the design tolerates a single link or device failure instead of having single points of failure
- Introduce **dynamic routing** (OSPF/EIGRP) between sites instead of relying solely on static routes, to make the branch/DMZ topology easier to scale
- Expand **logging and monitoring** so ACL denies and policy violations are visible and auditable, not just verified manually during testing
- Tighten ACLs further with **explicit deny-all statements and documented rule ordering** to reduce the risk of unintended permissive traffic
- Add **VLAN access port security** (port security, DHCP snooping, dynamic ARP inspection) to defend against spoofing and rogue devices at the access layer
- Document a **formal IP addressing and VLAN allocation table** that reserves room for future departments or sites without renumbering existing ones

## Running the Project

1. Install [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (free with a Cisco NetAcad account).
2. Clone or download this repository.
3. Open `team15.pkt` in Packet Tracer.
4. Use the topology view (`topology.png`) as a reference while exploring the network.
5. To verify behavior yourself:
   - Open a PC in a given VLAN and use `ping` or `tracert` to test intra-VLAN and inter-VLAN reachability.
   - From a Sales PC, attempt to reach the Business Application Server (10.207.50.20) — this should fail.
   - From a Branch Staff PC, attempt the same — this should succeed.
   - From a DMZ host, attempt to initiate a connection into any internal VLAN — this should fail.
   - From an external/outside host, attempt to reach the DMZ Web Server (10.207.100.10) — this should succeed.
6. Optional: review `configs.txt` for the running configuration of each network device.

## Video Demo

... This will be coming soon

## Repository Structure

```
team15-network/
├── team15.pkt
├── README.md
├── topology.png
└── configs.txt (optional)
```

## Objectives

- Implement VLAN-based network segmentation
- Design structured subnetting using /24 networks per department
- Enable inter-VLAN routing via gateway interfaces
- Deploy centralized internal services (DNS, Application Server)
- Configure a DMZ for external-facing services
- Enforce traffic control policies between network segments

## Configuration Summary

- VLANs configured for all departments (40–110)
- Trunk links configured between switches
- Inter-VLAN routing enabled via gateway interfaces
- Internal services hosted on the Services VLAN
- DMZ isolated for external-facing services
- ACLs applied for traffic filtering and access control
