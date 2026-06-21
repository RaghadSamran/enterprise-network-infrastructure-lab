# Troubleshooting Report

## Enterprise Network Infrastructure Lab

---

## Scenario 1 — OSPF Adjacency Failure

### Problem
OSPF neighborship between HQ-Router and Branch-Router dropped unexpectedly, causing loss of routing between HQ and Branch networks.

### Symptoms
- No OSPF neighbors visible in `show ip ospf neighbor`
- Branch network (192.168.40.0/24) unreachable from HQ
- Console log showed: `Nbr 192.168.40.1 from FULL to DOWN, Neighbor Down: Interface down or detached`

### Root Cause
WAN interface GigabitEthernet0/0/1 on HQ-Router was administratively shut down, breaking the point-to-point link between the two routers.

### Resolution Steps
1. Identified the fault using `show ip ospf neighbor` — empty neighbor table confirmed OSPF failure
2. Identified the downed interface using `show ip interface brief`
3. Re-enabled the interface:
   interface GigabitEthernet0/0/1
no shutdown
4. Verified OSPF convergence using `show ip ospf neighbor` — state returned to FULL/DR
5. Confirmed end-to-end connectivity restored via ping from IT-PC to Branch-Router

### Lesson Learned
Always verify interface status first when OSPF adjacency drops. A physically or administratively down interface is the most common cause of OSPF neighbor loss.

---

## Scenario 2 — DHCP Service Failure

### Problem
IT department workstations failed to obtain IP addresses automatically, causing network connectivity loss for all IT users.

### Symptoms
- IT-PC showed 0.0.0.0 when requesting DHCP
- `DHCP request failed` message on client
- No IP configuration received — gateway and DNS also missing

### Root Cause
The DHCP pool for the IT network (IT-Pool) was accidentally removed from HQ-Router configuration.

### Resolution Steps
1. Identified the issue by checking DHCP pools: `show running-config | section dhcp`
2. Confirmed IT-Pool was missing
3. Recreated the DHCP pool:
   ip dhcp pool IT-Pool

network 192.168.10.0 255.255.255.0

default-router 192.168.10.1

dns-server 8.8.8.8
4. Verified recovery — IT-PC successfully obtained 192.168.10.2 via DHCP
5. Confirmed full connectivity restored

### Lesson Learned
DHCP pool configuration should be backed up and version-controlled. Always verify pool existence when clients report IP assignment failures.

---

## Summary

| Scenario | Issue | Resolution |
|---|---|---|
| OSPF Adjacency Failure | WAN interface shutdown | Re-enabled interface, verified FULL/DR state |
| DHCP Service Failure | DHCP pool deleted | Recreated pool, verified client IP assignment |
