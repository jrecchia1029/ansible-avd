# floor1-member3

## Table of Contents

- [Management](#management)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [PTP](#ptp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [AAA Authorization](#aaa-authorization)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [802.1X Port Security](#8021x-port-security)
  - [802.1X Summary](#8021x-summary)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)

## Management

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 8.8.4.4 | IB_MGMT | - |
| 8.8.8.8 | IB_MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf IB_MGMT 8.8.4.4
ip name-server vrf IB_MGMT 8.8.8.8
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| pool.ntp.org | IB_MGMT | - | - | - | - | - | - | - | - |
| time.google.com | IB_MGMT | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server vrf IB_MGMT pool.ntp.org
ntp server vrf IB_MGMT time.google.com prefer
```

### PTP

#### PTP Summary

| Clock ID | Source IP | Priority 1 | Priority 2 | TTL | Domain | Mode | Forward Unicast |
| -------- | --------- | ---------- | ---------- | --- | ------ | ---- | --------------- |
| 00:1C:73:7f:00:05 | - | 127 | 5 | - | 127 | boundary | - |

#### PTP Device Configuration

```eos
!
ptp clock-identity 00:1C:73:7f:00:05
ptp priority1 127
ptp priority2 5
ptp domain 127
ptp mode boundary
ptp monitor threshold offset-from-master 250
ptp monitor threshold mean-path-delay 1500
ptp monitor sequence-id
ptp monitor threshold missing-message announce 3 sequence-ids
ptp monitor threshold missing-message delay-resp 3 sequence-ids
ptp monitor threshold missing-message follow-up 3 sequence-ids
ptp monitor threshold missing-message sync 3 sequence-ids
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| IB_MGMT | - | - |

#### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf IB_MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 <removed>
```

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **mstp**

#### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 57344 |

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
spanning-tree mst 0 priority 57344
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## VLANs

### VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 110 | IDF1-Data | - |
| 120 | IDF1-Voice | - |
| 130 | IDF1-Guest | - |
| 3000 | INBAND_MGMT | - |

### VLANs Device Configuration

```eos
!
vlan 110
   name IDF1-Data
!
vlan 120
   name IDF1-Voice
!
vlan 130
   name IDF1-Guest
!
vlan 3000
   name INBAND_MGMT
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet1 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet2 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet3 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet4 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet5 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet6 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet7 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet8 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet9 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet10 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet11 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet12 |  IDF1 Standard Port | trunk phone | - | 110 | - | - |
| Ethernet17 | FLOOR1-MEMBER1_Ethernet27 | *trunk | *110,120,130,3000 | *- | *- | 17 |
| Ethernet18 | FLOOR1-MEMBER2_Ethernet27 | *trunk | *110,120,130,3000 | *- | *- | 17 |

*Inherited from Port-Channel Interface

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet2
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet3
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet4
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet5
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet6
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet7
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet8
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet9
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet10
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet11
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet12
   description IDF1 Standard Port
   no shutdown
   switchport trunk native vlan 110
   switchport phone vlan 120
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 130
   dot1x reauthentication
   dot1x port-control auto
   dot1x host-mode multi-host authenticated
   dot1x mac based authentication
   dot1x timeout tx-period 3
   dot1x timeout reauth-period server
   dot1x reauthorization request limit 3
   spanning-tree portfast
   spanning-tree bpduguard enable
!
interface Ethernet17
   description FLOOR1-MEMBER1_Ethernet27
   no shutdown
   channel-group 17 mode active
!
interface Ethernet18
   description FLOOR1-MEMBER2_Ethernet27
   no shutdown
   channel-group 17 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel17 | FLOOR1-MEMBER1_Po27 | switched | trunk | 110,120,130,3000 | - | - | - | - | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel17
   description FLOOR1-MEMBER1_Po27
   no shutdown
   switchport
   switchport trunk allowed vlan 110,120,130,3000
   switchport mode trunk
```

### VLAN Interfaces

#### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan3000 | Inband Management | IB_MGMT | 1500 | False |

##### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan3000 |  IB_MGMT  |  11.11.11.8/24  |  -  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan3000
   description Inband Management
   no shutdown
   mtu 1500
   vrf IB_MGMT
   ip address 11.11.11.8/24
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| IB_MGMT | False |

#### IP Routing Device Configuration

```eos
no ip routing vrf IB_MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| IB_MGMT | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| IB_MGMT | 0.0.0.0/0 | 11.11.11.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf IB_MGMT 0.0.0.0/0 11.11.11.1
```

## Multicast

### IP IGMP Snooping

#### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

#### IP IGMP Snooping Device Configuration

```eos
```

## 802.1X Port Security

### 802.1X Summary

#### 802.1X Interfaces

| Interface | PAE Mode | State | Phone Force Authorized | Reauthentication | Auth Failure Action | Host Mode | Mac Based Auth | Eapol |
| --------- | -------- | ------| ---------------------- | ---------------- | ------------------- | --------- | -------------- | ------ |
| Ethernet1 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet2 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet3 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet4 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet5 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet6 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet7 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet8 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet9 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet10 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet11 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |
| Ethernet12 | authenticator | auto | - | True | allow vlan 130 | multi-host | True | - |

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| IB_MGMT | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance IB_MGMT
```
