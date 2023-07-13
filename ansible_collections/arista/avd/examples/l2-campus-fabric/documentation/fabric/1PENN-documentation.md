# 1PENN

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| 1PENN | leaf | 36EastIDF-A | - | 720XP | Provisioned | - |
| 1PENN | leaf | 36EastIDF-B | - | 720XP | Provisioned | - |
| 1PENN | leaf | 36EastIDF-Member1 | 172.100.100.103/24 | 720XP | Provisioned | - |
| 1PENN | leaf | 36EastIDF-Member2 | 172.100.100.104/24 | 720XP | Provisioned | - |
| 1PENN | leaf | 36EastIDF-Member3 | 172.100.100.104/24 | 720XP | Provisioned | - |
| 1PENN | leaf | 36WestIDF | - | 720XP | Provisioned | - |
| 1PENN | leaf | 37WestIDF-A | 172.100.100.103/24 | 720XP | Provisioned | - |
| 1PENN | leaf | 37WestIDF-B | 172.100.100.103/24 | 720XP | Provisioned | - |
| 1PENN | l3spine | SPLINE1 | 172.100.100.101/24 | 7050SX3 | Provisioned | - |
| 1PENN | l3spine | SPLINE2 | 172.100.100.102/24 | 7050SX3 | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| 1PENN | leaf | 36EastIDF-A | 11.11.11.6/24 | Vlan700 |
| 1PENN | leaf | 36EastIDF-B | 11.11.11.7/24 | Vlan700 |
| 1PENN | leaf | 36EastIDF-Member1 | 11.11.11.8/24 | Vlan700 |
| 1PENN | leaf | 36EastIDF-Member2 | 11.11.11.9/24 | Vlan700 |
| 1PENN | leaf | 36EastIDF-Member3 | 11.11.11.10/24 | Vlan700 |
| 1PENN | leaf | 36WestIDF | 11.11.11.4/24 | Vlan700 |
| 1PENN | leaf | 37WestIDF-A | 11.11.11.11/24 | Vlan700 |
| 1PENN | leaf | 37WestIDF-B | 11.11.11.12/24 | Vlan700 |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| leaf | 36EastIDF-A | Ethernet49 | l3spine | SPLINE1 | Ethernet2 |
| leaf | 36EastIDF-A | Ethernet51 | leaf | 36EastIDF-Member1 | Ethernet51 |
| leaf | 36EastIDF-A | Ethernet52 | leaf | 36EastIDF-Member2 | Ethernet51 |
| leaf | 36EastIDF-A | Ethernet58 | mlag_peer | 36EastIDF-B | Ethernet58 |
| leaf | 36EastIDF-A | Ethernet59 | mlag_peer | 36EastIDF-B | Ethernet59 |
| leaf | 36EastIDF-B | Ethernet50 | l3spine | SPLINE2 | Ethernet2 |
| leaf | 36EastIDF-B | Ethernet51 | leaf | 36EastIDF-Member1 | Ethernet52 |
| leaf | 36EastIDF-B | Ethernet52 | leaf | 36EastIDF-Member2 | Ethernet52 |
| leaf | 36EastIDF-Member1 | Ethernet53 | leaf | 36EastIDF-Member3 | Ethernet53 |
| leaf | 36EastIDF-Member2 | Ethernet53 | leaf | 36EastIDF-Member3 | Ethernet54 |
| leaf | 36WestIDF | Ethernet49 | l3spine | SPLINE1 | Ethernet1 |
| leaf | 36WestIDF | Ethernet50 | l3spine | SPLINE2 | Ethernet1 |
| leaf | 37WestIDF-A | Ethernet49 | l3spine | SPLINE1 | Ethernet3 |
| leaf | 37WestIDF-A | Ethernet50 | l3spine | SPLINE2 | Ethernet3 |
| leaf | 37WestIDF-A | Ethernet58 | mlag_peer | 37WestIDF-B | Ethernet58 |
| leaf | 37WestIDF-A | Ethernet59 | mlag_peer | 37WestIDF-B | Ethernet59 |
| leaf | 37WestIDF-B | Ethernet49 | l3spine | SPLINE1 | Ethernet4 |
| leaf | 37WestIDF-B | Ethernet50 | l3spine | SPLINE2 | Ethernet4 |
| l3spine | SPLINE1 | Ethernet49 | mlag_peer | SPLINE2 | Ethernet49 |
| l3spine | SPLINE1 | Ethernet50 | mlag_peer | SPLINE2 | Ethernet50 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.10.1.0/24 | 256 | 2 | 0.79 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| 1PENN | SPLINE1 | 10.10.1.1/32 |
| 1PENN | SPLINE2 | 10.10.1.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
