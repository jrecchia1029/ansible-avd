# floor3-leafa

## Table of Contents

- [Management](#management)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
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
| 310 | IDF3-Data | - |
| 320 | IDF3-Voice | - |
| 330 | IDF3-Guest | - |
| 3000 | INBAND_MGMT | - |

### VLANs Device Configuration

```eos
!
vlan 310
   name IDF3-Data
!
vlan 320
   name IDF3-Voice
!
vlan 330
   name IDF3-Guest
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
| Ethernet3/1 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/2 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/3 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/4 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/5 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/6 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/7 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/8 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/9 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/10 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/11 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/12 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/13 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/14 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/15 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/16 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/17 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/18 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/19 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/20 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/21 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/22 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/23 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/24 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/25 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/26 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/27 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/28 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/29 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/30 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/31 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/32 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/33 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/34 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/35 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/36 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/37 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/38 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/39 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/40 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/41 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/42 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/43 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/44 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/45 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/46 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/47 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet3/48 | SPINE1_Ethernet4 | *trunk | *310,320,330,3000 | *- | *- | 348 |
| Ethernet4/1 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/2 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/3 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/4 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/5 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/6 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/7 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/8 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/9 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/10 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/11 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/12 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/13 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/14 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/15 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/16 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/17 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/18 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/19 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/20 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/21 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/22 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/23 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/24 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/25 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/26 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/27 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/28 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/29 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/30 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/31 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/32 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/33 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/34 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/35 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/36 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/37 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/38 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/39 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/40 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/41 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/42 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/43 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/44 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/45 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/46 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/47 |  IDF2 Standard Port | trunk phone | - | 210 | - | - |
| Ethernet4/48 | SPINE2_Ethernet4 | *trunk | *310,320,330,3000 | *- | *- | 348 |

*Inherited from Port-Channel Interface

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet3/1
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/2
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/3
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/4
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/5
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/6
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/7
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/8
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/9
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/10
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/11
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/12
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/13
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/14
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/15
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/16
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/17
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/18
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/19
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/20
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/21
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/22
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/23
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/24
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/25
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/26
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/27
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/28
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/29
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/30
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/31
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/32
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/33
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/34
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/35
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/36
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/37
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/38
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/39
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/40
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/41
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/42
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/43
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/44
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/45
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/46
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/47
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet3/48
   description SPINE1_Ethernet4
   no shutdown
   channel-group 348 mode active
!
interface Ethernet4/1
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/2
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/3
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/4
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/5
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/6
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/7
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/8
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/9
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/10
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/11
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/12
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/13
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/14
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/15
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/16
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/17
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/18
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/19
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/20
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/21
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/22
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/23
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/24
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/25
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/26
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/27
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/28
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/29
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/30
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/31
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/32
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/33
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/34
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/35
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/36
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/37
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/38
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/39
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/40
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/41
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/42
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/43
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/44
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/45
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/46
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/47
   description IDF2 Standard Port
   no shutdown
   switchport trunk native vlan 210
   switchport phone vlan 220
   switchport phone trunk untagged
   switchport mode trunk phone
   switchport
   dot1x pae authenticator
   dot1x authentication failure action traffic allow vlan 230
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
interface Ethernet4/48
   description SPINE2_Ethernet4
   no shutdown
   channel-group 348 mode active
```

### Port-Channel Interfaces

#### Port-Channel Interfaces Summary

##### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel348 | SPINES_Po4 | switched | trunk | 310,320,330,3000 | - | - | - | - | - | - |

#### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel348
   description SPINES_Po4
   no shutdown
   switchport
   switchport trunk allowed vlan 310,320,330,3000
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
| Vlan3000 |  IB_MGMT  |  11.11.11.12/24  |  -  |  -  |  -  |  -  |  -  |

#### VLAN Interfaces Device Configuration

```eos
!
interface Vlan3000
   description Inband Management
   no shutdown
   mtu 1500
   vrf IB_MGMT
   ip address 11.11.11.12/24
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
| Ethernet3/1 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/2 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/3 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/4 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/5 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/6 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/7 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/8 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/9 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/10 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/11 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/12 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/13 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/14 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/15 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/16 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/17 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/18 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/19 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/20 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/21 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/22 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/23 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/24 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/25 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/26 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/27 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/28 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/29 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/30 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/31 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/32 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/33 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/34 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/35 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/36 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/37 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/38 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/39 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/40 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/41 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/42 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/43 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/44 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/45 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/46 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet3/47 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/1 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/2 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/3 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/4 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/5 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/6 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/7 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/8 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/9 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/10 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/11 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/12 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/13 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/14 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/15 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/16 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/17 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/18 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/19 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/20 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/21 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/22 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/23 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/24 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/25 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/26 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/27 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/28 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/29 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/30 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/31 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/32 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/33 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/34 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/35 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/36 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/37 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/38 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/39 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/40 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/41 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/42 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/43 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/44 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/45 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/46 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |
| Ethernet4/47 | authenticator | auto | - | True | allow vlan 230 | multi-host | True | - |

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
