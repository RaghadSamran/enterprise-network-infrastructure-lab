# Enterprise Network Infrastructure Lab

## Overview
A simulated multi-site enterprise network built in Cisco Packet Tracer, demonstrating real-world network design, configuration, and security implementation for a fictional company — TechCorp.

## Objectives
- Design a segmented enterprise network using VLANs
- Implement dynamic routing between multiple sites
- Configure core network services including DHCP and NAT
- Apply security controls using ACLs, SSH, and Port Security
- Validate network functionality through troubleshooting scenarios

## Network Topology
- **HQ Site:** 3 departments (IT, HR, Operations) connected via a Layer 2 switch with VLAN segmentation
- **Branch Site:** Branch Operations department connected via a dedicated router and switch
- **WAN Link:** Point-to-point connection between HQ-Router and Branch-Router (10.0.0.0/30)

## Technologies Implemented
| Technology | Purpose |
|---|---|
| VLANs (10, 20, 30, 40) | Department segmentation |
| Inter-VLAN Routing | Router-on-a-Stick configuration |
| OSPF | Dynamic routing between HQ and Branch |
| DHCP | Automatic IP assignment per department |
| NAT/PAT | Internet access simulation |
| ACLs | HR department blocked from IT resources |
| SSH | Secure remote device management |
| Port Security | Unauthorized device prevention |

## IP Addressing
| Network | Subnet | Gateway |
|---|---|---|
| IT (VLAN 10) | 192.168.10.0/24 | 192.168.10.1 |
| HR (VLAN 20) | 192.168.20.0/24 | 192.168.20.1 |
| Operations (VLAN 30) | 192.168.30.0/24 | 192.168.30.1 |
| Branch Operations (VLAN 40) | 192.168.40.0/24 | 192.168.40.1 |
| WAN Link | 10.0.0.0/30 | N/A |

## Security Implementation
- HR department cannot access IT resources (ACL enforced)
- SSH only allowed for remote management (Telnet disabled)
- Port security configured on IT port — unauthorized devices trigger shutdown
- NAT hides internal IP addresses from external networks

## Troubleshooting Scenarios

### OSPF Adjacency Failure
- Simulated WAN connectivity loss
- Verified OSPF neighbor relationship failure
- Restored connectivity and confirmed routing convergence

### DHCP Service Failure
- Removed DHCP pool configuration
- Verified client IP assignment failure
- Restored DHCP service and validated address allocation

## Skills Demonstrated
- Network Design
- VLAN Configuration
- Inter-VLAN Routing
- OSPF
- DHCP
- NAT/PAT
- Access Control Lists (ACLs)
- SSH Administration
- Port Security
- Network Troubleshooting

## Tools Used
- Cisco Packet Tracer 9.0
- GitHub (documentation)

## Repository Structure
├── README.md

├── Topology/        # Network topology diagram

├── Screenshots/     # Lab verification screenshots

├── Configurations/  # Device configuration files

└── Documentation/   # Troubleshooting report
