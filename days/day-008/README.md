# Day 008 — IPv4 Addressing, Part 2

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-16 | 7 min | Jeremy's IT Lab, Free CCNA: Day 8 (Network Devices) and Day 8 Lab (Packet Tracer Introduction) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided |

**Goal:** Set up the network by providing a router and the appropriate IP and Subnet Mask for the Routers interface.

## What I did

- [x] Guided: Worked out the IP addressing for the Day 9 Jeremy's IT Lab in Packet Tracer, and tested the traffic between computers.

## 🗺️ Topology

"evidence/008-topology.drawio.png"

Router 1
| Interface | Address | Mask |
|:--|:--|:--|:--|
| G0/0 | 15.255.255.254 | 255.0.0.0 |
| G0/1 | 182.98.255.254| 255.255.0.0 |
| G0/2 | 201.191.20.254 | 255.255.255.0 |

Hosts
| Host | Address | Mask | Connects to |
|:--|:--|:--|:--|
| PC1 | 15.0.0.1 | 255.0.0.0 |
| PC2 | 182.98.0.1 | 255.255.0.0 |
| PC3 | 201.191.20.1 | 255.255.255.0 |

## Lab Tasks

- [x] 1. Configure R1's hostname

- [x] 2. Use a 'show' command to view a list of R1's interfaces, their IP addresses, status, etc.

- [x] 3. Configure the appropriate IP addresses on R1's interfaces, and enable the interfaces
    Configure appropriate interface descriptions

- [x] 4. Use a 'show' command to verify R1's interfaces again.

- [x] 5. View the running config to confirm the configuration changes, then save the config

- [x] 6. Configure the IP addresses of PC1, PC2, and PC3
   (Watch the video to learn how to do this in Packet Tracer)

- [x] 7. Ping from PC1 to PC2 and PC3 to test connectivity

### Task 1 — Configure R1's Hostname

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
```

### Task 2 — Show R1's IP Satus

```
R1(config)#do show ip int br
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES unset  administratively down down 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
GigabitEthernet0/2     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
```

### Task 3 — Configure Interfaces

#### Interface 1: G0/0
```
R1(config)#int g0/0
R1(config-if)#ip add 15.255.255.254 255.0.0.0
R1(config-if)#desc
R1(config-if)#description ?
  LINE  Up to 240 characters describing this interface
R1(config-if)#description #PC1 Net Traffic
R1(config-if)#no shutdown

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up
```

#### Interface 2: G0/1
```
R1(config-if)#int g0/1
R1(config-if)#ip add 182.98.255.254 255.255.0.0
R1(config-if)#desc #PC2 Net Traffic
R1(config-if)#no shut

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
```

#### Interface 3: G0/2
```
R1(config-if)#int g0/2
R1(config-if)#ip add 201.191.20.254 255.255.255.0
R1(config-if)#descr
R1(config-if)#description #PC3 Net Traffic
R1(config-if)#no shutdow
R1(config-if)#no shutdown 

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/2, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/2, changed state to up
```
### Task 4 — Verify Configurations

```
R1(config-if)#exit
R1(config)#do show ip int br
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     15.255.255.254  YES manual up                    up 
GigabitEthernet0/1     182.98.255.254  YES manual up                    up 
GigabitEthernet0/2     201.191.20.254  YES manual up                    up 
Vlan1                  unassigned      YES unset  administratively down down
```

### Task 5 — View Running-Config and Save the Config

```
R1(config)#do show run
Building configuration...

Current configuration : 834 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
!
!
!
!
!
!
!
ip cef
no ipv6 cef
!
!
!
!
license udi pid CISCO2911/K9 sn FTX1524NMDP-
!
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0
 description #PC1 Net Traffic
 ip address 15.255.255.254 255.0.0.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 description #PC2 Net Traffic
 ip address 182.98.255.254 255.255.0.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/2
 description #PC3 Net Traffic
 ip address 201.191.20.254 255.255.255.0
 duplex auto
 speed auto
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
!
!
no cdp run
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R1(config)#do write mem
Building configuration...
[OK]
R1(config)#
```

### Task 6 — View Running-Config and Save the Config

> [!NOTE]
> The lab had the gateway addresses already pre-filled in. All I did was follow the the IP address schema provided and manually configure the IPv4 addresses of each PC.

### Task 7 — View Running-Config and Save the Config

"evidence/008-task-7"

## Evidence


## Command Cheat Sheet

<!-- Add each command or Packet Tracer tool you used, after you've used it. -->

| Command or tool | Where | What it does |
|:--|:--|:--|
| {{ }} | {{ }} | {{ }} |

## Synopsis

***Day 8 of Jeremy's IT Lab labs.***

IPv4 Addressing is probably my favorite part of the early learnings of Jeremy's IT Lab. This was a simple lab to complete from memory.

---

- `ipconfig` — check it against the addressing plan before trusting a ping
- Simulation mode — shows where a packet stops and why

**Previous:** [Day 007 · IPv4 Addressing, Part 1](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-007/README.md) | **Next:** Day 009 · Switch Interfaces
