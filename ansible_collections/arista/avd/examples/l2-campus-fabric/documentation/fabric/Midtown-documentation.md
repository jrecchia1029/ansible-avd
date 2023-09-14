# Midtown

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
| Midtown | leaf | floor1-leafa | - | 720XP-48ZC2 | Provisioned | - |
| Midtown | leaf | floor1-leafb | - | 720XP-48ZC2 | Provisioned | - |
| Midtown | leaf | floor1-member1 | - | 720XP-24ZY4 | Provisioned | - |
| Midtown | leaf | floor1-member2 | - | 720XP-24ZY4 | Provisioned | - |
| Midtown | leaf | floor1-member3 | - | 710XP-16P | Provisioned | - |
| Midtown | leaf | floor2-leafa | - | 720XP-48ZC2 | Provisioned | - |
| Midtown | leaf | floor2-leafb | - | 720XP-48ZC2 | Provisioned | - |
| Midtown | leaf | floor2-member1 | - | 720XP-24ZY4 | Provisioned | - |
| Midtown | leaf | floor3-leafa | - | 750X | Provisioned | - |
| Midtown | l3spine | spine1 | 172.100.100.101/24 | 7050SX3 | Provisioned | - |
| Midtown | l3spine | spine2 | 172.100.100.102/24 | 7050SX3 | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |
| Midtown | leaf | floor1-leafa | 11.11.11.4/24 | Vlan3000 |
| Midtown | leaf | floor1-leafb | 11.11.11.5/24 | Vlan3000 |
| Midtown | leaf | floor1-member1 | 11.11.11.6/24 | Vlan3000 |
| Midtown | leaf | floor1-member2 | 11.11.11.7/24 | Vlan3000 |
| Midtown | leaf | floor1-member3 | 11.11.11.8/24 | Vlan3000 |
| Midtown | leaf | floor2-leafa | 11.11.11.9/24 | Vlan3000 |
| Midtown | leaf | floor2-leafb | 11.11.11.10/24 | Vlan3000 |
| Midtown | leaf | floor2-member1 | 11.11.11.11/24 | Vlan3000 |
| Midtown | leaf | floor3-leafa | 11.11.11.12/24 | Vlan3000 |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| leaf | floor1-leafa | Ethernet51 | mlag_peer | floor1-leafb | Ethernet51 |
| leaf | floor1-leafa | Ethernet52 | mlag_peer | floor1-leafb | Ethernet52 |
| leaf | floor1-leafa | Ethernet53/1 | l3spine | spine1 | Ethernet1 |
| leaf | floor1-leafa | Ethernet53/2 | leaf | floor1-member1 | Ethernet25 |
| leaf | floor1-leafa | Ethernet54/1 | l3spine | spine2 | Ethernet1 |
| leaf | floor1-leafa | Ethernet54/2 | leaf | floor1-member2 | Ethernet25 |
| leaf | floor1-leafb | Ethernet53/1 | l3spine | spine1 | Ethernet2 |
| leaf | floor1-leafb | Ethernet53/2 | leaf | floor1-member1 | Ethernet26 |
| leaf | floor1-leafb | Ethernet54/1 | l3spine | spine2 | Ethernet2 |
| leaf | floor1-leafb | Ethernet54/2 | leaf | floor1-member2 | Ethernet26 |
| leaf | floor1-member1 | Ethernet27 | leaf | floor1-member3 | Ethernet17 |
| leaf | floor1-member2 | Ethernet27 | leaf | floor1-member3 | Ethernet18 |
| leaf | floor2-leafa | Ethernet51 | mlag_peer | floor2-leafb | Ethernet51 |
| leaf | floor2-leafa | Ethernet52 | mlag_peer | floor2-leafb | Ethernet52 |
| leaf | floor2-leafa | Ethernet53/1 | l3spine | spine1 | Ethernet3 |
| leaf | floor2-leafa | Ethernet53/2 | leaf | floor2-member1 | Ethernet25 |
| leaf | floor2-leafb | Ethernet53/1 | l3spine | spine2 | Ethernet3 |
| leaf | floor2-leafb | Ethernet53/2 | leaf | floor2-member1 | Ethernet26 |
| leaf | floor3-leafa | Ethernet3/48 | l3spine | spine1 | Ethernet4 |
| leaf | floor3-leafa | Ethernet4/48 | l3spine | spine2 | Ethernet4 |
| l3spine | spine1 | Ethernet49 | mlag_peer | spine2 | Ethernet49 |
| l3spine | spine1 | Ethernet50 | mlag_peer | spine2 | Ethernet50 |

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
| Midtown | spine1 | 10.10.1.1/32 |
| Midtown | spine2 | 10.10.1.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
