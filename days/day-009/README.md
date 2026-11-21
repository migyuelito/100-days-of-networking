# Day 009 — Switch Interfaces

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-21 | 15 min | Jeremy's IT Lab, Free CCNA: Day 9 (Switch Interfaces) and Day 9 Lab (Configuring Interfaces) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided |

**Goal:** Set up Packet Tracer, rebuild the Day 1 topology from memory, and prove where a subnet boundary stops traffic, even on a single switch.21

## What I did

- [x] Guided: followed the Day 9 Lab

## Topology

"evidence/009-topology.drawio.png"

| Host | Address | Mask |
|---|---|---|
| PC1 | 192.168.1.10 | 255.255.255.0 |
| PC2 | 192.168.1.20 | 255.255.255.0 |
| PC3 | 192.168.2.10 | 255.255.255.0 |

## Lab Tasks

- [x] 1. Configure the hostname of R1, SW1, and SW2

- [x] 2. Configure the appropriate IP addresses on R1, PC1, PC2, PC3, PC4

- [x] 3. Manually configure the speed and duplex on interfaces connected to other 
    networking devices (not end hosts)

- [x] 4. Configure appropriate descriptions on each interface

- [x] 5. Disable interfaces which are not connected to other devices

### Task 1 - Configure Networking Device Hostnames

> Configure the routers hostname.
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
R1(config)#
```

> Configure Switch 1 hostname.
```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW1
SW1(config)#
```

> Configure Switch 2 hostname.
```
Switch>en
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname SW2
SW2(config)#
```

### Task 2 - Configure IP Addresses

> Configure the routers IP address.
```
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#int g0/0
R1(config-if)#ip add 172.16.255.254 255.255.0.0
R1(config-if)#no shutdown

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up
```

> Configure the PC1 - PC4 IP addresses.
| Host | Address | Mask |
|---|---|---|
| PC1 | 172.16.0.1 | 255.255.0.0 |
| PC2 | 172.16.0.2 | 255.255.0.0 |
| PC3 | 172.16.0.3 | 255.255.0.0 |
| PC4 | 172.16.0.4 | 255.255.0.0 |

### Task 3

> Configure Router's speed and duplex
```
R1#en
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#int g0/0
R1(config-if)#speed 1000
R1(config-if)#duplex full
R1(config-if)#
```

> Configure Switch 1 speed and duplex
```
SW1#en
SW1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW1(config)#int g0/1
SW1(config-if)#exit
SW1(config)#int range g0/1 - 2
SW1(config-if-range)#speed 1000
SW1(config-if-range)#duplex full
SW1(config-if-range)#int range f0/1 - 2
SW1(config-if-range)#speed 1000
                              ^
% Invalid input detected at '^' marker.
	
SW1(config-if-range)#speed 100
SW1(config-if-range)#duplex ?
  auto  Enable AUTO duplex configuration
  full  Force full duplex operation
  half  Force half-duplex operation
SW1(config-if-range)#duplex full
SW1(config-if-range)#
```

> Configure Switch 2 speed and duplex
```
SW2>en
SW2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW2(config)#int g0/1
SW2(config-if)#speed 1000
SW2(config-if)#duplex full
SW2(config-if)#int range f0/1 - 2
SW2(config-if-range)#speed 100
SW2(config-if-range)#duplex half
SW2(config-if-range)#
```
### Task 4 - Configure descriptions

> Router interface
```
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#int g0/0
R1(config-if)#description ## To Switch 1 ##
R1(config-if)#
```

> Switch 1 interface
```
SW1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW1(config)#int g0/1
SW1(config-if)#desc ## To Router 1 ##
SW1(config-if)#int g0/2
SW1(config-if)#desc ## To Switch 2 ##
SW1(config-if)#
```

> Switch 2 interface
```
SW2#
%SYS-5-CONFIG_I: Configured from console by console

SW2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW2(config)#int g0/1
SW2(config-if)#desc ## To Switch 1 ##
SW2(config-if)#
```

### Task 5 - Disable non-connected interfaces

> Router 1 Interfaces
```
R1#
R1#sh ip int br
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     172.16.255.254  YES manual up                    up 
GigabitEthernet0/1     unassigned      YES unset  administratively down down 
GigabitEthernet0/2     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
R1#
```
> [!Note] Router 1 had already disabled interfaces.

> Switch 1 Interfaces
```
SW1>en
SW1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW1(config)#do show ip int br
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual up                    up 
FastEthernet0/3        unassigned      YES manual down                  down 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual down                  down 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual down                  down 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
FastEthernet0/22       unassigned      YES manual down                  down 
FastEthernet0/23       unassigned      YES manual down                  down 
FastEthernet0/24       unassigned      YES manual down                  down 
GigabitEthernet0/1     unassigned      YES manual up                    up 
GigabitEthernet0/2     unassigned      YES manual up                    up 
Vlan1                  unassigned      YES manual administratively down down
SW1(config)#int range f0/3 - 24
SW1(config-if-range)#shutdown

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/5, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/7, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/9, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/11, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/12, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/13, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/14, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/15, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/16, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/17, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/18, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/19, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/20, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/21, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/22, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/23, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down
SW1(config-if-range)#desc ## Unused Port ##
SW1(config-if-range)#
```

> Switch 2 Interfaces
```
SW2#
SW2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
SW2(config)#do show ip int br
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual up                    up 
FastEthernet0/3        unassigned      YES manual down                  down 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual down                  down 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual down                  down 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
FastEthernet0/22       unassigned      YES manual down                  down 
FastEthernet0/23       unassigned      YES manual down                  down 
FastEthernet0/24       unassigned      YES manual down                  down 
GigabitEthernet0/1     unassigned      YES manual up                    up 
GigabitEthernet0/2     unassigned      YES manual down                  down 
Vlan1                  unassigned      YES manual administratively down down
SW2(config)#int range f0/3 - 24
SW2(config-if-range)#shutdown

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/5, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/7, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/8, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/9, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/11, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/12, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/13, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/14, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/15, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/16, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/17, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/18, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/19, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/20, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/21, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/22, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/23, changed state to administratively down

%LINK-5-CHANGED: Interface FastEthernet0/24, changed state to administratively down
SW2(config-if-range)#desc ## Unused Port ##
SW2(config-if-range)#int g0/2
SW2(config-if)#shutdown

%LINK-5-CHANGED: Interface GigabitEthernet0/2, changed state to administratively down
SW2(config-if)#desc ## Unused Port ##
SW2(config-if)#
```

## Evidence

evidence.R1-running-config.txt
evidence.SW1-running-config.txt
evidence.SW2-running-config.txt


## Synopsis

***Day 9 of Jeremy's IT Lab labs.***
Similar to previous days about configuring IP addresses. Don't get too manage a lot of switch interfaces, so this was a good review.

**Previous Day:** Day 008 · **Next:** Day 010
