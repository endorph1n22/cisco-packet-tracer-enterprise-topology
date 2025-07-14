![Network Topology](topology.png)
# Cisco Packet Tracer Network Project

## 📡 Overview

This project simulates a multi-segment enterprise network using **Cisco Packet Tracer**, featuring:
- Multiple VLANs
- Inter-VLAN routing via subinterfaces
- **OSPF** dynamic routing
- **Centralized DHCP server** with relay configuration
- **Access Control Lists (ACL)** for traffic filtering
- Proper switching (Access + Trunk ports with VLAN tagging)

---

## 🧱 Topology Summary

- **R1**, **R2**, and **R3** connect user VLANs and route traffic between them via OSPF.
- **R4** acts as a core router and connects to the **DHCP Server (7.7.7.7)**.
- Each router has a directly connected switch (**S1, S2, S3**) configured with access ports for VLANs.
- All routers are in **OSPF Area 0**.

---

## 📶 VLAN and Subnet Overview

| VLAN    | Subnet            | Default Gateway     | Location (Router) |
|---------|-------------------|---------------------|-------------------|
| VLAN 10 | 192.168.10.0/24   | 192.168.10.1        | R1                |
| VLAN 20 | 192.168.20.0/24   | 192.168.20.1        | R1                |
| VLAN 30 | 192.168.30.0/24   | 192.168.30.1        | R1                |
| VLAN 10 | 172.16.10.0/24    | 172.16.10.1         | R2                |
| VLAN 20 | 172.16.20.0/24    | 172.16.20.1         | R2                |
| VLAN 30 | 172.16.30.0/24    | 172.16.30.1         | R2                |
| VLAN 10 | 10.10.0.0/24      | 10.10.0.1           | R3                |
| VLAN 20 | 10.20.0.0/24      | 10.20.0.1           | R3                |
| VLAN 30 | 10.30.0.0/24      | 10.30.0.1           | R3                |
| Server  | 7.7.7.0/28        | 7.7.7.1             | R4 (DHCP Server)  |

---

## 🔧 Routing

- **OSPF Process ID**: 10
- All routers participate in **OSPF Area 0**
- Internal VLAN subnets and point-to-point links are advertised
- Full mesh routing between R1, R2, R3, and R4

---

## 📨 DHCP Configuration

- A centralized **DHCP server** (IP: `7.7.7.7`) serves all VLANs
- Routers use `ip helper-address 7.7.7.7` on each relevant interface
- DHCP pools:

| Pool Name   | Subnet          | Gateway        | Start IP         |
|-------------|------------------|----------------|------------------|
| 192vlan10   | 192.168.10.0/24  | 192.168.10.1   | 192.168.10.100   |
| 192vlan20   | 192.168.20.0/24  | 192.168.20.1   | 192.168.20.100   |
| 192vlan30   | 192.168.30.0/24  | 192.168.30.1   | 192.168.30.100   |
| 172vlan10   | 172.16.10.0/24   | 172.16.10.1    | 172.16.10.100    |
| 172vlan20   | 172.16.20.0/24   | 172.16.20.1    | 172.16.20.100    |
| 172vlan30   | 172.16.30.0/24   | 172.16.30.1    | 172.16.30.100    |
| 10vlan10    | 10.10.0.0/24     | 10.10.0.1      | 10.10.0.100      |
| 10vlan20    | 10.20.0.0/24     | 10.20.0.1      | 10.20.0.100      |
| 10vlan30    | 10.30.0.0/24     | 10.30.0.1      | 10.30.0.100      |
| serverPool  | 7.7.7.0/28       | 0.0.0.0        | 7.7.7.0          |

---

## 🛡 ACL Configuration

Each router applies **ACL 111** on outbound interfaces to:
- Restrict inter-VLAN access
- Permit DHCP traffic to/from `7.7.7.7`
- Allow specific VLAN-to-VLAN communication
- Prevent unauthorized subnet traversal

---

## 🧪 Switching

Each switch (S1, S2, S3):
- Has access ports assigned to VLANs 10–30
- Trunk port (`GigabitEthernet0/2`) connects to its respective router
- PVST (Per-VLAN Spanning Tree) enabled

---

## 📂 Files

- `.pkt` file: Cisco Packet Tracer project
- `README.md`: Project documentation (you are here)
- Configs: See individual device configs inside Packet Tracer

---

## ✅ How to Use

1. Open the `.pkt` file in Cisco Packet Tracer.
2. Start simulation or real-time mode.
3. Verify DHCP assignment to PCs.
4. Test inter-VLAN and inter-site connectivity.
5. Optionally test ACL behavior using `ping`/`traceroute`.

---

## 📌 Notes

- Ensure DHCP server is turned on and configured with matching pools.
- All PCs should receive IPs via DHCP automatically.
- ACLs may block certain routes—adjust as needed for testing.
