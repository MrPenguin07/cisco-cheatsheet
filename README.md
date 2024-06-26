# Cisco Cheatsheet
## PRs with additional topics or changes are welcome!
### Cisco CLI Reference, Howtos, and Tools

Credit to the original author [@grplyler](https://github.com/grplyler)  
Expanded upon by [@MrPenguin07](https://github.com/MrPenguin07)

***Added new sections***
- [X] Syslog, Restore firmware, Rollback with `revert`
- [X] BGP, OSPF, Added [Cisco-send](https://github.com/MrPenguin07/cisco-send)
- [X] Spanning-tree, SPAN, TFTP, DHCP `ip helper-address`
- [X] Diagnosing issues, Useful cmds, ZBF

***To-Do***
- [ ] ACLs
- [ ] Device auth.
- [ ] RIPv2
- [ ] GRE/IPSEC
- [ ] HSRP/GLBP
- [ ] SNMP
- [ ] VOIP
- [ ] NAT
- [ ] Static routing

## Quick Navigation

### General Sections
  * [Basic Networking](#basic-networking)
  * [Intermediate Networking](#intermediate-networking)
  * [Advanced Networking](#advanced-networking)
  * [Monitoring/Logging](#monitoring-logging)
  * [Useful Commands](#useful-commands)
  * [Diagnostics](#diagnostics)
  * [How To's](#how-tos)
  * [Tools](#tools)

## Full Navigation

  * [Basic Networking](#basic-networking)
    + [Setup](#setup)
      - [Initialize](#initialize)
      - [Basic Switch Config](#basic-switch-config)
      - [Basic Router Config](#basic-router-config)
      - [Basic Config with Password Security](#basic-config-with-password-security)
      - [Basic Security](#basic-security)
      - [Configure SSH](#configure-ssh)
      - [Set Clock](#set-clock)
      - [Basic Hardening (Work Needed)](#basic-hardening-work-needed)
      - [Backup config over FTP](#backup-config-over-ftp)
      - [Backup config over console](#backup-config-over-console)
      - [Restore Config](#restore-config)
    + [Interfaces](#interfaces)
      - [Interface Selection](#interface-selection)
      - [Assign Static IP to Interface](#assign-static-ip-to-interface)
      - [Interface Ranges](#interface-ranges)
    + [Interface Verification](#interface-verification)
      - [Remove IP Addresses](#remove-ip-addresses)
    + [Console Port](#console-port)
      - [Change Console Baudrate](#change-console-baudrate)
    + [DHCP](#dhcp)
      - [Snippet: Enable Router DHCP Server](#snippet-enable-router-dhcp-server)
      - [Snippet: Enable Switch DHCP Server](#snippet-enable-switch-dhcp-server)
      - [Create DHCP Pool](#create-dhcp-pool)
      - [DHCP Verification](#dhcp-verification)
      - [Configuring IP Helper-Address](#configuring-ip-helper-address)
      - [Disable DHCP](#disable-dhcp)
      - [Re-enabled DHCP](#re-enabled-dhcp)
      - [Create VLAN DHCP](#create-vlan-dhcp)
      - [Verify DHCP Pool](#verify-dhcp-pool)
      - [Delete DHCP Pool](#delete-dhcp-pool)
---
  * [Intermediate Networking](#intermediate-networking)
    + [VLANs](#vlans)
      - [VLAN Creation](#vlan-creation)
      - [Port Assignment](#port-assignment)
      - [IP Assignemnt](#ip-assignemnt)
      - [Verification](#verification)
      - [Voice and Data VLAN](#voice-and-data-vlan)
      - [Management VLAN](#management-vlan)
      - [Delete VLANS on file](#delete-vlans-on-file)
      - [Delete VLANS in memory](#delete-vlans-in-memory)
      - [Inter-VLAN Routing](#inter-vlan-routing)
    + [Trunks](#trunks)
      - [Create multi-switch vlan trunk](#create-multi-switch-vlan-trunk)
      - [Trunk Verification](#trunk-verification)
    + [EtherChannel](#etherchannel)
      - [Configure EtherChannel](#configure-etherchannel)
      - [Verify EtherChannel](#verify-etherchannel)
    + [DTP (Dynamic Trunking Protocol)](#dtp-dynamic-trunking-protocol)
      - [Configure DTP](#configure-dtp)
      - [Disable DTP](#disable-dtp)
      - [Verify DTP](#verify-dtp)
    + [Spanning Tree Protocol (STP)](#spanning-tree-protocol)
      - [Basic STP Configuration](basic-stp-configuration)
        * [Enable STP](#enable-stp)
        * [Set STP mode](#set-stp-mode)
      - [STP Priority and Root Bridge Configuration](stp-priority-and-root-bridge-configuration)
        * [Set Bridge priority](#set-bridge-priority)
        * [Set Bridge priority for all VLANs](#set-bridge-priority-for-all-vlans)
        * [Root Bridge Configuration](#root-bridge-configuration)
      - [STP Verification and Troubleshooting](#stp-verification-and-troubleshooting)
    + [Zone-Based Firewalls](#zone-based-firewalls)
      - [Understanding Zone-Based Firewalls](#understanding-zone-based-firewalls)
      - [Defining Zones](#defining-zones)
      - [Creating Class Maps](#creating-class-maps)
      - [Creating Policy Maps](#creating-policy-maps)
      - [Applying Policy to Zone Pairs](#applying-policy-to-zone-pairs)
      - [Assigning Interfaces to Zones](#assigning-interfaces-to-zones)
      - [Verifying Zone-Based Firewall Configuration](#verifying-zone-based-firewall-configuration)
---
  * [Advanced Networking](#advanced-networking)
    + [OSPFv2](#ospfv2)
      - [OSPF Router IDs](#ospf-router-ids)
        * [All Commands](#all-commands)
        * [Enable router OSPF process](#enable-router-ospf-process)
        * [Configure Loopback](#configure-loopback)
        * [Configure OSPF Router ID](#configure-ospf-router-id)
        * [Modify OSPF router ID](#modify-ospf-router-id)
      - [OSPF - Point-to-Point Networks](#ospf---point-to-point-networks)
        * [Network Command Syntax](#network-command-syntax)
        * [Configure OSPF With Network Command](#configure-ospf-with-network-command)
        * [Use Entire Gigabit Interfaces](#use-entire-gigabit-interfaces)
        * [Configure OSPF with `ip ospf`](#configure-ospf-with-ip-ospf)
        * [OSPF Passive Interfaces](#ospf-passive-interfaces)
        * [Find Designated Router and Backup](#find-designated-router-and-backup)
        * [Change OSPF from Broadcast to Point-to-Point](#change-ospf-from-broadcast-to-point-to-point)
        * [Loopback and P2P Networks](#loopback-and-p2p-networks)
      - [Multiaccess OSPF Networks](#multiaccess-ospf-networks)
        * [Configure OSPF Priority](#configure-ospf-priority)
      - [Modifying Single Area OSPF](#modifying-single-area-ospf)
        * [Adjusting Reference Bandwidth](#adjusting-reference-bandwidth)
        * [Manually Set OSPF Link Cost](#manually-set-ospf-link-cost)
        * [Show OSPF Hello Packet Intervals](#show-ospf-hello-packet-intervals)
        * [Set OSPF Hello Packet Intervals](#set-ospf-hello-packet-intervals)
        * [Set OSPF Dead Interval](#set-ospf-dead-interval)
      - [OSPF Default Routes](#ospf-default-routes)
        * [Propogate Default Route](#propogate-default-route)
        * [Verify Propogated Default Route](#verify-propogated-default-route)
      - [Verify Single-Area OSPF](#verify-single-area-ospf)
        * [Verify OSPF Neighbors](#verify-ospf-neighbors)
        * [Verify OSPF Protocols](#verify-ospf-protocols)
        * [Verify OSPF Process Info](#verify-ospf-process-info)
        * [Verify OSPF Interface Setting](#verify-ospf-interface-setting)
    * [BGP](#bgp)
      + [Basic BGP Configuration](#basic-bgp-configuration)
        - [Enable BGP Process](#enable-bgp-process)
        - [Define BGP Neighbor](#define-bgp-neighbor)
      + [Viewing BGP Information](#viewing-bgp-information)
        - [Show BGP Summary](#show-bgp-summary)
        - [Show BGP Routing Table](#show-bgp-routing-table)
      + [Advertising Networks](#advertising-networks)
        - [Advertise Network](#advertise-network)
      + [Configuring Route Aggregation](#configuring-route-aggregation)
        - [Aggregate Routes](#aggregate-routes)
    * [Redistribute Routes](#redistributing-routes)
      - [Redistribute Static/BGP Routes](#redistribute-static-routes)
      - [Redistribute OSPF Routes](#redistribute-ospf-routes)
---        
  * [Monitoring/Logging](#monitoring-logging)
    + [SPAN - Switched Port Analyzer Configuration](#span-configuration)
      - [Configure SPAN](#configure-span)
        * [RSPAN Configuration](#rspan-configuration)
        * [Configure RSPAN](#configure-rspan)
        * [Verify SPAN/RSPAN](#verify-spanrspan)
    + [Syslog](#syslog)
      - [Syslog Configuration](#syslog-configuration)
        * [Configure Syslog Server](#configure-syslog-server)
        * [Set Syslog Level](#set-syslog-level)
        * [Verify Syslog Configuration](#verify-syslog-configuration)
---
  * [Useful Commands](#useful-commands)
    + [Using Pipes in IOS](#using-pipes-in-ios)
      - [Understanding Pipe Usage](#understanding-pipe-usage)
      - [Include Keyword](#include-keyword)
      - [Exclude Keyword](#exclude-keyword)
      - [Section Keyword](#section-keyword)
      - [Begin Keyword](#begin-keyword)
    + [Prevent Syslog Message Interruptions](#prevent-syslog-message-interruptions)
    + [Prevent DNS Resolution for Typos](#prevent-dns-resolution-for-typos)
    + [Set Message of the Day Banner](#set-message-of-the-day-banner)
    + [Create Command Alias](#create-command-alias)
    + [Disable TCP and UDP Small Servers](#disable-tcp-and-udp-small-servers)
    + [Add Description to Interfaces](#add-description-to-interfaces)
    + [Show CPU Processes](#show-cpu-processes)
    + [Enable Terminal Monitoring](#enable-terminal-monitoring)
---
  * [Diagnostics](#diagnostics)
    + [BGP Troubleshooting](#bgp-troubleshooting)
      - [Show BGP Summary](#show-bgp-summary)
      - [Show BGP Neighbors](#show-bgp-neighbors)
    + [OSPF Troubleshooting](#ospf-troubleshooting)
      - [Show OSPF Neighbors](#show-ospf-neighbors)
      - [Show OSPF Interface](#show-ospf-interface)
    + [Common Diagnostics](#common-diagnostics)
      - [Show Running Configuration](#show-running-configuration)
      - [Show Interface Brief](#show-interface-brief)
      - [Show IP DHCP Binding](#show-ip-dhcp-binding)
      - [Show Access-Lists](#show-access-lists)
      - [Show EIGRP Neighbors](#show-eigrp-neighbors)
      - [Show Version](#show-version)
      - [Show NTP Status](#show-ntp-status)
      - [Show ARP](#show-arp)
      - [Show MAC Address-Table](#show-mac-address-table)
    + [Port and VLAN Information](#port-and-vlan-information)
      - [Show VLAN](#show-vlan)
      - [Show Interfaces Trunk](#show-interfaces-trunk)
    + [Protocol Specific](#protocol-specific)
      - [Show IP NAT Translations](#show-ip-nat-translations)
      - [Show Standby](#show-standby)
    + [EtherChannel and Port Security](#etherchannel-and-port-security)
      - [Show EtherChannel](#show-etherchannel)
      - [Show Port-Security](#show-port-security)
    + [CDP Diagnostics](#cdp-diagnostics)
---         
  * [How To's](#how-tos)
    + [FTP Server Usage](#ftp-server-usage)
    + [Sending Local Config over Serial](#sending-local-config-over-serial)
    + [Configure Serial Port with `stty` on Linux](#configure-serial-port-with-stty-on-linux)
    + [Firmware & Recovery](#firmware-and-recovery)
      - [Nuking (ROMMON, Password Recovery, etc)](#nuking-rommon-password-recovery-etc)
      - [Restoring Firmware](#restoring-firmware)
        * [Copying Firmware to Device](#copying-firmware-to-device)
        * [Via TFTP](#via-tftp)
        * [Via FTP](#via-ftp)
      - [Copying Firmware from Device](#copying-firmware-from-device)
        * [To TFTP Server](#to-tftp-server)
        * [To FTP Server](#to-ftp-server)
    + [Configuration Rollback Using Revert](#configuration-rollback-using-revert)
      - [Setup Archive Feature](#setup-archive-feature)
      - [Initiate Rollback Timer](#initiate-rollback-timer)
      - [Reset Rollback Timer](#reset-rollback-timer)
      - [Manual Rollback](#manual-rollback)
      - [Cancel Rollback](#cancel-rollback)
---      
  * [Tools](#tools)
    + [Subnetting/Calcuation](#subnettingcalcuation)
      - [ipcalc (*nix)](#ipcalc-nix)
      - [whatmask (*nix)](#whatmask-nix)
    
## Basic Networking

### Setup
---

#### Initialize

These commands wipe all config and reboot the device

```
erase startup-config
delete vlan.dat
reload
```
**Note:** Remember to say "no" to saving running config on reload. If you say yes, running config will be saved and you wont be working with fresh config on reload.

#### Basic Switch Config

```
configure terminal
no ip domain-lookup
hostname S1
line console 0
logging synchronous
exit
banner motd $ Authorized Access Only! And Godzilla will beat Kong any day $
exit
copy running-config startup-config
```

#### Basic Router Config

```
configure terminal
no ip domain-lookup
hostname R1
line console 0
logging synchronous
exit
banner motd $ Authorized Access Only! And Godzilla will beat Kong any day $
exit
copy running-config startup-config
```

#### Basic Config with Password Security

```
configure terminal
no ip domain-lookup
hostname R1
line console 0
logging synchronous
exit
banner motd $ Authorized Access Only! And Godzilla will beat Kong any day $
exit
copy running-config startup-config
conf t
enable secret class
line console 0
password cisco
login
exit
line vty 0 4
password cisco
login
exit
service password-encryption
end
copy running-config startup-config
```

#### Basic Security

```
conf t
enable secret class
line console 0
password cisco
login
exit
line vty 0 4
password cisco
login
exit
service password-encryption
end
```

#### Configure SSH

```
show ip ssh
conf t
ip domain-name cisco.com
crypto key generate rsa

username admin secret ccna
line vty 0 15
transport input ssh
login local
exit
ip ssh version 2
exit
```

#### Set Clock

*Show Clock*

```
show clock
```

*Sets clock to eastern US time*

```
clock timezone EST -5
```

*Revert to Default Timezone*

```
no clock timezone
```

#### Basic Hardening (Work Needed)

```
conf t
! Logout timer
!
line con 0
 exec-timeout 5
line vty 0 4
 exec-timeout 5
 
exit

ip ssh time-out 60
ip ssh authentication-retries 3
end
```

#### Backup config over FTP

*Using included [FTP server](#ftp-server-usage)*

```
copy running-config startup-config
copy startup-config ftp://192.168.1.10/config.txt
```

#### Backup config over console

A simple yet effective method here is to;
```
set terminal length 0
show run
```
Highlight and copy paste to local machine. Perhaps set terminal length back to ~25 so the less pager works again.

#### Restore Config
```
copy ftp://192.168.1.10/config.txt running-config
```

### Interfaces
---


#### Interface Selection

*Assign an IP address to a port*
```
conf t
int f0/1
ip addr 192.168.10.11 255.255.255.0
end
```

#### Assign Static IP to Interface

```
cont t
int g0/0
ip addr 10.0.0.10 255.255.255.0
```

#### Interface Ranges

*Assign and IP address to a port*
```
conf t
int f0/1
ip addr 192.168.10.11 255.255.255.0
end
```

*Select Single Range and Assign to a VLAN*
```
conf t
int range f0/1-12
switchport mode access
switch access vlan 10
end
```

```
conf t
int range f0/13-24
switchport mode access
switchport access vlan 20
end
```

*Select Multiple Interface Ranges and Move to a VLAN*
```
conf t
int range f0/1-4,g0/1,f0/16-20
switchport mode access
switchport access vlan 10
end
```

### Interface Verification

```
show ip interface brief
```
*or*
```
show ip int br
```

#### Remove IP Addresses

```
conf t
int f0/1
no ip addr
end
```

### Console Port

#### Change Console Baudrate

```
conf t
line con 0
speed 115200
end
```

```
conf t
line con 0
speed 9600
end
```

### DHCP
---

#### Snippet: Enable Router DHCP Server

This snippet configures a DHCP Server on R1 and will hand out
IPs on the `10.0.0.1/24` network. Great for using an [FTP Server](#ftp-server-usage) with.

```
conf t
ip domain name cisco.com
ip dhcp excluded-address 10.0.0.1
ip dhcp pool test
network 10.0.0.0 255.255.255.0
default-router 10.0.0.1
end
```

#### Snippet: Enable Switch DHCP Server

```
ip dhcp pool test
network 10.0.0.0 255.255.255.0
domain-name cisco.com
default-router 10.0.0.1
dns-server 10.0.0.1
lease 4
ip dhcp snooping
ip dhcp-server 10.0.0.3
interface vlan 1
ip address 10.0.0.3
```

#### Create DHCP Pool

*Workaround for CCNA labs at Liberty University since we can't change the LAB IP addresses*

```
conf t
ip domain name cisco.com
ip dhcp excluded-address 10.0.0.1
ip dhcp pool managementpool
network 10.0.0.1 255.255.255.0
default-router 10.0.0.1
end
```

```
conf t
ip dhcp excluded-address 192.168.10.1
ip dhcp excluded-address 192.168.10.254
ip dhcp pool office-pool-1
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.5.5
domain-name linux.org
end
```

#### DHCP Verification

```
# show running-config | section dhcp
# show ip dhcp binding
# show ip dhcp server statistics
```

#### Configuring IP Helper-Address

The `ip helper-address` command is used on a router's interface to enable forwarding of DHCP broadcasts onto other networks.   
It allows clients on a subnet without a DHCP server to reach the DHCP server on another subnet.

```
conf t
# interface <interface_type> <interface_number>
# ip helper-address <dhcp_server_ip>
```
Configure the IP helper-address on the interface that receives the DHCP requests, specifying the IP address of the DHCP server.

##### Verifying IP Helper-Address
```
# show ip interface <interface_type> <interface_number>
```
This command checks the configuration of the ip helper-address on a specific interface to ensure it's correctly set to the DHCP server's IP address.  


#### Disable DHCP

```
conf t
no service dhcp
end
```

#### Re-enabled DHCP

```
conf t
service dhcp
end
```

#### Create VLAN DHCP

*Creates a Seperate DHCP Pool for each VLAN*

*Create VLANS*
```
conf t
vlan 10
name Management
vlan 20
name Sales
vlan 30
name Operations
end
```

*Configure SVI's and IP Address*

| VLAN | IP Address | Gateway |
|------|------------|--------|
| 10   | 192.168.10.254 | 192.168.10.1 |
| 20 | 192.168.20.254 | 192.168.20.1 |
| 30 | 192.168.30.254 | 192.168.30.1 |

```
conf t
int vlan 10
ip address 192.168.10.254 255.255.255.0
ip default-gateway 192.168.10.1
no shut

int vlan 20
ip address 192.168.20.254 255.255.255.0
ip default-gateway 192.168.20.1
no shut

int vlan 30
ip address 192.168.30.254 255.255.255.0
ip default-gateway 192.168.30.1
no shut
end
```

*Add interfaces to VLANS, 8 ports per vlan*

```
conf t
int range f0/1-7
switchport mode access
switchport access vlan 10

int range f0/8-15
switchport mode access
switchport access vlan 20

int range f0/16-24
switchport mode access
switchport access vlan 30
end
```

*Create DHCP Pools for each vlan*

```
conf t
ip domain name cisco.com
ip dhcp excluded-address 192.168.10.1
ip dhcp pool vlan10pool
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
import all


ip dhcp excluded-address 192.168.20.1
ip dhcp pool vlan20pool
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
import all

ip dhcp excluded-address 192.168.30.1
ip dhcp pool vlan30pool
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
import all
end
```

Now when a device plugs into a port `f0/4` for instance and performs a DHCP request, it should get an IP like `192.168.10.3` because it is plugged into the ports assigned to VLAN 10

#### Verify DHCP Pool

```
show ip dhcp pool
```

#### Delete DHCP Pool

```
conf t
no ip dhcp pool managementpool
end
```

## Intermediate Networking

### VLANs
---

#### VLAN Creation

```
conf t
vlan 10
name Faculty
exit
```

```
conf t
vlan 20
name Students
exit
```

#### Port Assignment

```
conf t
interface range Fa0/1-12
switchport mode access
switchport access vlan 10
end
```

```
conf t interface range Fa0/13-24
switchport mode access
switchport access vlan 20
end
```

```
conf t
interface Gi0/1
switchport mode access
switchport access vlan 99
end
```

#### IP Assignemnt

```
cont t
int vlan 99
ip address 10.0.0.1 255.255.255.0
end
```

#### Verification

```
show vlan brief
```

#### Voice and Data VLAN

*Assuming Data on VLAN 10, Voice on VLAN 20*

```
conf t
int Fa0/4
switchport mode access
switchport access vlan 10
switchport voice vlan 20
end
```

#### Management VLAN

```
conf t
vlan 99
name Management
exit
interface Fa0/24
switchport mode access
switchport access vlan 99
exit
int vlan 99
ip addr 10.0.0.1 255.255.255.0
end
```

#### Delete VLANS on file

```
delete vlan.dat
```

#### Delete VLANS in memory
*Warning: Make sure you move ports to another vlan or the will be unsable*

```
conf t
no vlan 10
no vlan 20
end
```

#### Inter-VLAN Routing

*Creates multiple sub-interfaces on a router port to enable inter-vlan routing.*

*Note: `encapsulation dot1q` must be called on a sub interface before an IP can be assigned to it.*

```
conf t
interface G0/0/1.10
description Default Gateway for VLAN 10
encapsulation dot1Q 10
ip add 192.168.10.1 255.255.255.0
exit

interface G0/0/1.20
description Default Gateway for VLAN 20
encapsulation dot1Q 20
ip addr 192.168.20.1 255.255.255.0
exit

interface G0/0/1.99
description Default Gateway for VLAN 99
encapsulation dot1Q 99
ip addr 192.168.99.1 255.255.255.0
exit

interface G0/0/1
description Trunk link to S1
no shut
end
```

### Trunks
---

#### Create multi-switch vlan trunk

*S1*

```
conf t
interface Gi0/1
description Trunk Line to S2 Gi0/1
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 99
end
```

*Note: Remember to set the native vlan (to 99 for instance) on each switch in the trunk so you don't get a native vlan mismatch warning*

#### Trunk Verification

```
show interface trunk
show interface g0/1 switchport
```

### EtherChannel
---

Etherchannel protocols LACP and PAgP configure multiple physical interfaces and links to act as one logical one. You can configure up to 8 ports to act as a single link. This increases bandwidth and improves redundancy.

*Note: `mode active` sets the etherchannel group to use the LACP protocol*

#### Configure EtherChannel

*Configure etherchannel between two switches connected with two ethernet cables.*
```
conf t
int range f0/1-2
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
switchport trunk allowed vlan 1,2,20
```


#### Verify EtherChannel

```
show interfaces trunk
show etherchannel summary
```

### DTP (Dynamic Trunking Protocol)
---

#### Configure DTP

```
conf t
int gi0/1
switchport mode dynamic auto
end
```

**or**

```
conf t
int gi0/1
switchport mode dynamic desirable
end
```


#### Disable DTP

*Usefull for connecting to devices that don't support Cisco propietary DTP or creating a static trunk*

```
conf t
int gi0/1
switchport mode trunk
switchport nonegotiate
end
```

#### Verify DTP

```
show dtp interface gi0/1
```

### Spanning Tree Protocol
---
#### Basic STP Configuration
##### Enable STP

```
conf t
spanning-tree vlan <vlan_id>
```
Where <vlan_id> is the VLAN ID for which STP is being configured.

##### Set STP Mode
```
spanning-tree mode { pvst | rapid-pvst | mst }
```
Choose pvst for Per-VLAN Spanning Tree, rapid-pvst for Rapid Per-VLAN Spanning Tree, or mst for Multiple Spanning Tree.

#### STP Priority and Root Bridge Configuration
##### Set Bridge Priority
```
spanning-tree vlan <vlan_id> priority <priority_value>
```
Where <vlan_id> is the VLAN ID, and <priority_value> is the priority value (0, 4096, 8192, 12288, ..., 61440).

##### Set Bridge Priority for All VLANs
```
spanning-tree vlan 1-4094 priority <priority_value>
```

##### Root Bridge Configuration
```
spanning-tree vlan <vlan_id> root {primary|secondary}
```
This command configures the current switch as the root bridge for the specified VLAN.

#### STP Verification and Troubleshooting
`show spanning-tree`  
`show spanning-tree vlan <vlan_id>`  
`show spanning-tree interface <interface_type> <interface_number> detail`  

### Zone-Based Firewalls
---
#### Understanding Zone-Based Firewalls

Zone-Based Firewalls in Cisco IOS are advanced security features that allow you to create different security zones in your network and apply specific policies to control the traffic flow between these zones.

#### Defining Zones
```
conf t
# zone security <zone_name>
```
This command is used to define a security zone. Each zone represents a segment of your network. Replace <zone_name> with a descriptive name for the zone.

#### Creating Class Maps
```
class-map type inspect match-any <class_map_name>
match protocol <protocol>
```
Class maps are used to classify traffic based on specific criteria. The match protocol command allows you to specify which protocol you want to match, like HTTP, FTP, or others.   
To view the list of protocols available for inspection, you can use the show policy-map type inspect protocol command. This command will list all protocols that the firewall can inspect.

#### Creating Policy Maps
```
policy-map type inspect <policy_map_name>
class type inspect <class_map_name>
inspect
```
Policy maps are where you define the actions to be taken on the traffic classified by the class maps. The inspect action, for example, enables stateful inspection of the traffic.  
This stateful inspection allows the firewall to keep track of active sessions and make decisions based on the state of these sessions.

#### Applying Policy to Zone Pairs
```
zone-pair security <zone_pair_name> source <source_zone> destination <destination_zone>
service-policy type inspect <policy_map_name>
```
After defining your class maps and policy maps, you need to apply them to a zone pair. This command specifies the source and destination zones and applies the policy map to control traffic between these zones.

#### Assigning Interfaces to Zones
```
conf t
# interface <interface_type> <interface_number>
zone-member security <zone_name>
```

This command is used to assign an interface on your device to a specific security zone, effectively placing that interface within the defined security context.

#### Verifying Zone-Based Firewall Configuration
```
# show zone security
# show policy-map type inspect zone-pair sessions
```
Use these commands to verify your configuration. The first command shows the defined security zones, while the second displays active sessions based on your policy maps.


## Advanced Networking

### Routing

#### OSPFv2

#### OSPF Router IDs
##### All Commands

```
show ip ospf neighbor
show ip ospf database 
```

##### Enable router OSPF process

Starting Mode: Global, Non-enabled

```
enable
conf t
router ospf 10
```

##### Configure Loopback

```
enable
conf t
interface Loopback 1
ip addr 1.1.1.1 255.255.255.255
end
```

##### Configure OSPF Router ID

_replace `1.1.1.1` with desired id_
```
conf t
router ospf 10
router-id 1.1.1.1
end
```

##### Modify OSPF router ID

_Prompt confirmation with 'y' needed_

```
conf t
router ospf 10
router-id 1.1.1.2
end
clear ip ospf process
```

_Verify_

```
show ip proto | include Router ID
```
#### OSPF - Point-to-Point Networks

##### Network Command Syntax

`Router(config-router)# network network-address wildcard-mask area area-id`

##### Configure OSPF With Network Command

The following configures a trianngle of 3 routers connected to
each other as an OSPF point to point network.

```
conf t
router ospf 10
network 10.10.1.0 0.0.0.255 area 0
network 10.10.1.4 0.0.0.3 area 0
network 10.10.1.12 0.0.0.3 area 0
end
```

##### Use Entire Gigabit Interfaces

```
conf t
router ospf 10
network 10.10.1.1 0.0.0.0 area 0
network 10.10.1.5 0.0.0.0 area 0
network 10.10.1.14 0.0.0.0 area 0
end
```

##### Configure OSPF with `ip ospf`

Configure OSPF directly on the interfaces rather with with the network
command.

Syntax: `Router(config-if)# ip ospf <process-id> area <area-id>`

```
R1(config)# router ospf 10
R1(config-router)# no network 10.10.1.1 0.0.0.0 area 0
R1(config-router)# no network 10.1.1.5 0.0.0.0 area 0
R1(config-router)# no network 10.1.1.14 0.0.0.0 area 0
R1(config-router)# interface GigabitEthernet 0/0/0
R1(config-if)# ip ospf 10 area 0
R1(config-if)# interface GigabitEthernet 0/0/1 
R1(config-if)# ip ospf 10 area 0
R1(config-if)# interface Loopback 0
R1(config-if)# ip ospf 10 area 0
R1(config-if)#
```

##### OSPF Passive Interfaces

```
conf t
router ospf 10
passive-interface loopback 0
end
```

```
conf t
router ospf 10
passive-interface Gi0/0/0
end
```

##### Find Designated Router and Backup

```
show ip ospf interface GigabitEthernet 0/0/0
```

##### Change OSPF from Broadcast to Point-to-Point

```
conf t
interface GigabitEthernet 0/0/0
ip ospf network point-to-point
```

##### Loopback and P2P Networks

Loobacks can be used to simulate real LAN networks

```
conf t
interface Loopback 0
ip ospf network point-to-point
```

```
show ip route | include 10.10.1
```

#### Multiaccess OSPF Networks

##### Configure OSPF Priority

```
conf t
int g0/0/1
ip ospf priority 255
end
```

Where `255` can be values from `0` to `255` with higher numbers making the router to be elected `DR`.

#### Modifying Single Area OSPF

##### Adjusting Reference Bandwidth

```
Router# router ospf 10
Router(config-router) auto-cost reference bandwidth 1000
```

_Where 1000 is the speed of the link in Mpbs_
Common Values: 10, 100, 1000

##### Manually Set OSPF Link Cost

```
conf t
int g0/0/1
ip ospf cost 25
interface l0
ip ospf cost 15
end
```

##### Show OSPF Hello Packet Intervals

```
show ip ospf int g0/0/1
```

##### Set OSPF Hello Packet Intervals

```
Router(config-if)# ip ospf hello-interval <seconds>
```

```
conf t
int g0/0/1
ip ospf hello-interval 30
end
```

Note: dead-interval automatically gets set as `hello-interval * 4`


##### Set OSPF Dead Interval

#### OSPF Default Routes

##### Propogate Default Route

```
conf t
ip route 0.0.0.0 0.0.0.0 loopback 1
router ospf 10
default-information originate
```

##### Verify Propogated Default Route

```
show ip route | begin Gateway
```

#### Verify Single-Area OSPF

##### Verify OSPF Neighbors

```
show ip ospf neighbor
```

##### Verify OSPF Protocols

```
show ip protocols
```

##### Verify OSPF Process Info

```
show ip ospf
```

##### Verify OSPF Interface Setting

```
show ip ospf int g0/0/1
show ip ospf int brief
```

Where `g0/0/1` is the interface you was to see OSPF information on.

```
conf t
int g0/0/1
ip ospf dead-interval 100
end
```
### BGP
---
#### Basic BGP Configuration

##### Enable BGP Process
```
conf t
router bgp <AS_number>
bgp router-id <router_id>
```
Where `<AS_number>` is the Autonomous System number for the router and `<router_id>` is the desired router ID, typically formatted as an IP address.

##### Define BGP Neighbor
```
conf t
router bgp <AS_number>
neighbor <neighbor_IP> remote-as <remote_AS_number>
```
Where `<neighbor_IP>` is the IP address of the BGP neighbor and `<remote_AS_number>` is the Autonomous System number of the BGP neighbor.

#### Viewing BGP Information

##### Show BGP Summary
```
show ip bgp summary
```

##### Show BGP Routing Table
```
show ip bgp
```

#### Advertising Networks

##### Advertise Network
```
conf t
router bgp <AS_number>
network <network_address> mask <subnet_mask>
```
Where `<network_address>` is the network you want to advertise and `<subnet_mask>` is the subnet mask for the network.

#### Configuring Route Aggregation

##### Aggregate Routes
```
conf t
router bgp <AS_number>
aggregate-address <aggregate_address> <aggregate_mask>
```
Where `<aggregate_address>` is the summarized network address and `<aggregate_mask>` is the subnet mask for the summarized network.

### Redistributing Routes

#### Redistribute Static Routes
```
conf t
router bgp <AS_number>
redistribute static
```
Where <AS_number> is the Autonomous System number for the router.

#### Redistribute OSPF Routes
```
conf t
router bgp <AS_number>
redistribute ospf <process_id>
```
Where <AS_number> is the Autonomous System number for the router, and <process_id> is the OSPF process ID.

#### Redistribute Connected Routes
```
conf t
router bgp <AS_number>
redistribute connected
```
Where <AS_number> is the Autonomous System number for the router.

#### Verify Redistribution
```
show ip bgp
```

## Monitoring Logging

### SPAN Configuration
#### Configure SPAN

Create a SPAN session to monitor traffic:
```
conf t
monitor session <session_number> source interface <interface_type> <interface_number>
monitor session <session_number> destination interface <interface_type> <interface_number>
```
Can monitor a port/range, a VLAN or range of VLANs etc.

### RSPAN Configuration
#### Configure RSPAN
Create an RSPAN VLAN, then configure the source and destination sessions:
```
conf t
vlan <vlan_id>
remote-span
exit
monitor session <session_number> source remote vlan <vlan_id>
monitor session <session_number> destination interface <interface_type> <interface_number>
```

### Verify SPAN+RSPAN
```
show monitor session <session_number>
```

## Syslog
### Syslog Configuration

#### Configure Syslog Server

Set the address of the Syslog server and enable logging:
```
conf t
logging host <syslog_server_ip>
logging on
```
Where <syslog_server_ip> is the IP address of your Syslog server.

#### Set Syslog Level
```
conf t
logging trap <level>
```
Where <level> can be one of the following: emergencies, alerts, critical, errors, warnings, notifications, informational, debugging.

#### Verify Syslog Configuration
```
show logging
```

## Useful Commands

### Using Pipes in IOS

#### Understanding Pipe Usage
Pipes ( | ) in Cisco IOS are used to filter the output of commands, making it easier to find specific information.

#### Include Keyword
```
<command> | include <expression>
```
Filters the output to only show lines that include the specified expression.

#### Exclude Keyword
```
<command> | exclude <expression>
```
Filters the output to remove lines that contain the specified expression.

#### Section Keyword
```
<command> | section <expression>
```
Displays the output section that includes the specified expression. Particularly useful for commands that have a structured output like show running-config.

#### Begin Keyword
```
<command> | begin <expression>
```
Displays the output starting from the line where the specified expression first appears, which is useful for quickly navigating to a specific part of the command output.

### Prevent Syslog Message Interruptions
```
conf t
# line con 0
# logging synchronous
```
This command prevents console messages from interrupting command input by synchronizing log messages.

### Prevent DNS Resolution for Typos
```
conf t
no ip domain-lookup
```
Disables DNS lookup to prevent the router from attempting to translate incorrectly entered commands as domain names.

### Set Message of the Day Banner
```
conf t
banner motd # [Your Message Here] #
```
Sets a message-of-the-day banner that appears on all connected terminals. Replace [Your Message Here] with your desired text.

### Create Command Alias
```
conf t
alias exec [shortcut] [command]
```
Creates a shortcut (alias) for a longer command. Replace [shortcut] with your alias and [command] with the command it represents.

### Disable TCP and UDP Small Servers
```
conf t
no service tcp-small-servers
no service udp-small-servers
```
Disables TCP and UDP small servers, which are often unnecessary and can be a security risk.

### Add Description to Interfaces
```
conf t
interface [interface_type] [interface_number]
description [text]
```
Adds a description to an interface. Replace [interface_type] and [interface_number] with the specific interface details and [text] with the description.

### Show CPU Processes
```
# show processes cpu
# show processes memory
```
Displays information about the router's CPU/mem processes and their utilization.

### Enable Terminal Monitoring
```
# terminal monitor
```
Enables the display of log and debug command output on your terminal. Useful in SSH or Telnet sessions.


## Diagnostics

### BGP Troubleshooting

#### Show BGP Summary

```
# show ip bgp summary
```
This command provides a snapshot of the BGP routing process, displaying the number of BGP routes and the status of BGP peers.  
Example output includes a list of BGP neighbors, the AS number, the last time the BGP peer was up, and the state of the BGP session (e.g., Established).

#### Show BGP Neighbors

```
# show ip bgp neighbors
```
Use this command to get detailed information about each BGP neighbor, such as BGP state, configured timers, and counters for messages sent and received.  
The output will give you insights into the BGP session's performance and help identify any configuration mismatches between neighbors.

### OSPF Troubleshooting

#### Show OSPF Neighbors

```
# show ip ospf neighbor
```
This command confirms if OSPF has formed adjacency with neighbors and shows the current state of each neighbor relationship.  
The output details each OSPF neighbor's router ID, state (e.g., Full for a complete adjacency), and the interface it's connected on.

#### Show OSPF Interface

```
# show ip ospf interface
```
To diagnose OSPF interface-specific issues, such as problems with timers or MTU mismatches, use this command.  
The output includes the cost, state, and neighbors connected to each OSPF-enabled interface, providing a comprehensive look at how OSPF is operating on the router.

### Common Diagnostics

#### Show Running Configuration

```
# show running-config
```
This command displays the current active configuration in the device's memory. It's useful for verifying changes that have not yet been saved to the startup configuration.  

#### Show Interface Brief

```
# show ip interface brief
```
The output from this command provides a concise table of interfaces, showing their IP addresses, statuses, and protocol states, which is helpful for a quick check of interface operations.  

#### Show IP DHCP Binding

```
# show ip dhcp binding
```
This displays the list of all IP addresses assigned by the DHCP server to clients, along with their MAC addresses, lease time, and type of binding.

#### Show Access-Lists

```
# show access-lists
```
Shows all configured access lists and their conditions. It's a quick way to review which access control entries are configured and how many packets matched each entry.

#### Show EIGRP Neighbors

```
# show ip eigrp neighbors
```
Useful for verifying EIGRP-established adjacencies, this command shows neighboring routers connected via EIGRP and includes details such as the hold time and last heard timer.  

#### Show Version

```
# show version
```
Displays the router or switch's hardware model, software version, names and sources of configuration files, the last reboot reason, and additional information about the hardware platform.

#### Show NTP Status

```
# show ntp status
```
This command is used to verify the status of NTP synchronization on the device.   
It tells you if the device is synchronized with an NTP server, the stratum level, and the reference IP address of the NTP source.
Network Utilities


#### Show ARP

```
# show arp
```
Show arp provides the Address Resolution Protocol (ARP) table of the device.   
It maps IP addresses to MAC addresses for all interfaces, which is crucial for troubleshooting network connectivity issues.

#### Show MAC Address-Table

```
# show mac address-table
```
This command displays the MAC address table, which contains all learned MAC addresses and their associated VLAN and port information.  
It's essential for diagnosing issues with MAC address learning and switch port mappings.


### Port and VLAN Information

#### Show VLAN
```
# show vlan
# show vlan int br
```
This command displays information about the VLANs currently running in the switch, including VLAN ID, name, and the ports assigned to them.   
Useful for verifying VLAN configurations.

#### Show Interfaces Trunk

```
# show interfaces trunk
```
Lists the trunking status of interfaces, showing the native VLAN and the allowed VLANs on each trunk port.

### Protocol Specific

#### Show IP NAT Translations

```
# show ip nat translations
```
Displays the Network Address Translation (NAT) translations table, helpful for troubleshooting NAT configurations by showing active translation entries.

#### Show Standby

```
# show standby
```
Used to display the status of Hot Standby Router Protocol (HSRP) configurations, showing the state, priority, and the IP address of the standby router.

### EtherChannel and Port Security

#### Show EtherChannel
```
# show etherchannel summary
```
Provides an overview of the EtherChannel status, including the group number, ports involved, and their status, which is key in verifying link aggregation setups.

#### Show Port-Security

```
# show port-security
```
Displays the port security configuration on interfaces, including the maximum number of secure MAC addresses, current count of secure MAC addresses, and security violation counts.

#### CDP Diagnostics

Cisco Discovery Protocol (CDP) is a proprietary Layer 2 protocol used by Cisco devices to discover information about directly connected devices, such as model, port number, and IP address.
```
# show cdp neighbors
```
This command lists all directly connected Cisco devices. Useful for network topology mapping and troubleshooting connectivity issues.
```
# show cdp interface <interface_name>
```
Displays CDP information specific to a particular interface, including the frequency of CDP updates and the hold time for CDP packets.


## How To's

### FTP Server Usage

1. Clone the repo: 

    ```
    git clone https://github.com/MrPenguin07/cisco-cheatsheet
    cd !$
    ```
    
2. Install python requirements (for ftp server):

    ```
    pip install -r requirements.txt
    ```
    
3. Run python ftp_server.py

    ```
    python3 ftp_server.py
    ```
    
4. Pull a script onto a network device (WARNING: Backup to avoid any losses)

    ```
    Switch#> copy ftp://192.168.1.10/sw_base.txt running-config
    ```
    
    *Replace 192.168.1.10 with the IP of the computer connected to the switch or router.*


### Configure Serial Port with `stty` on Linux

Set the default configuration with stty to cisco console default, 9600 bps, 8N1, no flow control:

```
stty -F /dev/ttyUSB0 9600 litout -crtscts
```

or:

```
stty -F /dev/ttyUSB0 cs8 -parenb -cstopb -echo raw speed 9600

 # What the arguments mean:
 #   cs8:     8 data bits
 #   -parenb: No parity (because of the '-')
 #   -cstopb: 1 stop bit (because of the '-')
 #   -echo: Without this option, Linux will sometimes automatically send back
 #          any received characters, even if you are just reading from the serial
 #          port with a command like 'cat'. Some terminals will print codes
 #          like "^B" when receiving back a character like ASCII ETX (hex 03).
 ```


## Firmware and Recovery

### Nuking (ROMMON, Password Recovery, etc)

*Perform a Boot Interupt to Recover a lost or unknown password*

**WARNING**: This operation will delete all current config on the device

1. Ensure Console Cable is connected at 9600 Baudrate
2. Backup config if you need
3. Unplug Power
4. Wait for a few seconds
5. Re-insert the power cord to the switch
6. Within 15 seconds, hold the `Mode` button until the green flashing light flashes amber and then returns to flashing green. Release the `Mode` button.
7. Something like the following should display:

    ```
    initialize the flash file system, and finish loading the operating system software#
    
    flash_init
    load_helper
    boot
    ```
8. Run `flash_init`
9. Run `copy flash:config.text flash:config.text.old`
10. Run `boot`

    The device should now boot with no config and grant you access to it.

### Restoring Firmware

Set up a local FTP/TFTP server, there's a simple python script included [here](#ftp-server-usage)

#### Copying Firmware to Device

#### Via TFTP
Transfer firmware to the device using a TFTP server:

```
conf t
copy tftp: flash:
address or name of remote host []? <tftp_server_ip>
source filename []? <firmware_filename>
destination filename []? <firmware_filename>
```
Replace <tftp_server_ip> with the IP address of your TFTP server, and <firmware_filename> with the name of the firmware file.

#### Via FTP

Transfer firmware to the device using an FTP server:
```
conf t
copy ftp: flash:
address or name of remote host []? <ftp_server_ip>
username []? <username>
password []? <password>
source filename []? <firmware_filename>
destination filename []? <firmware_filename>
```
Replace <ftp_server_ip> with the IP address of your FTP server, <username> and <password> with your FTP credentials, and <firmware_filename> with the name of the firmware file.

### Copying Firmware from Device

#### To TFTP Server

Transfer firmware from the device to a TFTP server:
```
conf t
copy flash: tftp:
source filename []? <firmware_filename>
address or name of remote host []? <tftp_server_ip>
```
Replace <firmware_filename> with the name of the firmware file, and <tftp_server_ip> with the IP address of your TFTP server.

#### To FTP Server

Transfer firmware from the device to an FTP server:
```
conf t
copy flash: ftp:
source filename []? <firmware_filename>
address or name of remote host []? <ftp_server_ip>
username []? <username>
password []? <password>
```
Replace <firmware_filename> with the name of the firmware file, <ftp_server_ip> with the IP address of your FTP server, and <username> and <password> with your FTP credentials.



### Console Access with Screen on Linux

For this you will need a USB console cable. These can be picked up
on amazon for about $9-$12.

1. Connect your the USB console cable from the computers usb port to the cisco RJ-45 console port.

2. Install the `screen` program if you dont already have it.

```
apt install screen
```

3. Find the USB device.

If its the first USB serial device you plugged in, it should be `/dev/ttyUSB0`. The second one should be `/dev/ttyUSB1`, etc.

You can verify with with `ls /dev | grep USB`

4. Run `screen`

You will need root access or preferably to add your user into the `dialout` group (true for most linux distros I believe).

```
screen /dev/ttyUSB0
```

Running with a specific baudrate.

```
screen /dev/ttyUSB0 9600
screen /dev/ttyUSB0 115200
```

To exit screen, hit `Ctrl-a`, `Ctrl-d`

If you have trouble with the connection, e.g. it lags or is funky, cisco serial connections require the following settings by default:

- `9600` baud
- `8` data bits
- `no` parity
- `1` stop bit
- `no` flow control

To do that exactly with screen:
```
screen /dev/ttyS0 9600,cs8,-parenb,-cstopb,-hupcl
screen /dev/ttyS0 19200,cs8,-parenb,-cstopb,-hupcl
screen /dev/ttyS0 115200,cs8,-parenb,-cstopb,-hupcl
```

With `odd` parity:
```
screen /dev/ttyS0 9600,cs8,parenb,parodd,-cstopb,-hupcl
```

With `even` parity:
```
screen /dev/ttyS0 9600,cs8,parenb,-parodd,-cstopb,-hupcl
```

### Sending Local Config over Serial

See [@MrPenguin](https://github.com/MrPenguin07)'s cisco-send repository;
[cisco-send](https://github.com/MrPenguin07/cisco-send)

### Linux File Transfer Over Console (minicom / xmodem)

_Howto coming soon!_

### Windows File Transfer Over Console ( HyperTerminal / xmodem)

_Howto coming soon!_  
(actually it won't, not by me, accepting PR heh)

## Configuration Rollback Using Revert

### Setup Archive Feature

To enable configuration archiving and set the storage path.  
Set the archive path where config files will be saved.
```
Router# conf t
Router(config)# archive
Router(config-archive)#path ?
flash: Write archive on flash: file system
ftp: Write archive on ftp: file system
http: Write archive on http: file system
https: Write archive on https: file system
pram: Write archive on pram: file system
rcp: Write archive on rcp: file system
scp: Write archive on scp: file system
tftp: Write archive on tftp: file system
Router(config-archive)# path flash:
Router(config-archive)# end
```

### Initiate Rollback Timer  

Example how to start a rollback timer (e.g., 1 minute),  
make changes then revert.
```
Router# configure terminal revert timer 1
Router(config)# hostname I-Changed-This
I-Changed-This(config)# end
```

### Reset Rollback Timer

To reset or extend the rollback timer (e.g., add 20 minutes):

```
Router# configure revert timer 20
```

### Manual Rollback

To force a manual rollback to the archived configuration:

```
Router# conf t
Router(config)# hostname I-Changed-This
I-Changed-This(config)# end
I-Changed-This# configure revert now
Router#
````

### Cancel Rollback

After thoroughly testing changes,  
you may cancel the rollback process:

```
Router# configure confirm
```
Remember, these commands should be used with caution and tested during maintenance windows to prevent unexpected behaviour.

## Tools

### Subnetting/Calcuation

#### ipcalc (*nix)
In most distro's package repositories; something resembling `<package manager> install ipcalc`
```
$ tldr ipcalc

  Perform simple operations and calculations on IP addresses and networks.
  More information: <https://manned.org/ipcalc>.

  Show information about an address or network with a given subnet mask:
     $ ipcalc 1.2.3.4 255.255.255.0
  Show information about an address or network in CIDR notation:
     $ ipcalc 1.2.3.4/24
  Show the broadcast address of an address or network:
     $ ipcalc -b 1.2.3.4/30
  Show the network address of provided IP address and netmask:
     $ ipcalc -n 1.2.3.4/24
  Display geographic information about a given IP address:
     $ ipcalc -g 1.2.3.4
```
**Example**
```
$ ipcalc 1.2.3.4/24

ipcalc 1.2.3.4/24
Address:   1.2.3.4              00000001.00000010.00000011. 00000100
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   1.2.3.0/24           00000001.00000010.00000011. 00000000
HostMin:   1.2.3.1              00000001.00000010.00000011. 00000001
HostMax:   1.2.3.254            00000001.00000010.00000011. 11111110
Broadcast: 1.2.3.255            00000001.00000010.00000011. 11111111
Hosts/Net: 254                   Class A
```

#### whatmask (*nix)
In most distro's package repositories; something resembling `<package manager> install whatmask`

**Example**

```
$ whatmask 10.0.1.12/30

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 10.0.1.12
CIDR = ........................: /30
Netmask = .....................: 255.255.255.252
Netmask (hex) = ...............: 0xfffffffc
Wildcard Bits = ...............: 0.0.0.3
------------------------------------------------
Network Address = .............: 10.0.1.12
Broadcast Address = ...........: 10.0.1.15
Usable IP Addresses = .........: 2
First Usable IP Address = .....: 10.0.1.13
Last Usable IP Address = ......: 10.0.1.14
```
