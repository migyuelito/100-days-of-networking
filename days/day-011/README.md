# Day 011 — Packet Tracer setup and the subnet boundary

<!-- Pre-drafted plan. Fill in every {{ }} with what you actually did and saw, tick the boxes you completed, and delete lines you didn't do. -->

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-24 | 13 min | Jeremy's IT Lab, Free CCNA: Day 11 (Routing Fundamentals & Static Routing) and Day 11 Lab (Configuring Static Routes) & (Troubleshooting Static Routes) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | **Guided** |

**Goal:** Configure static routes and troubleshoot static routes.

## What I did

- [x] Guided: Followed the Day 11 Configuring static routes lab instructions in Packet Tracer to set static routes.
- [x] Guided: Followed the Day 11 troubleshooting static routes lab instructions in Packet Tracer to troubleshoot static routes

## Topology

evidence/config-static-routes/011-topology.drawio.png

## Lab Tasks

All devices have NO pre-configurations:

- [ ] 1. Configure the PCs and routers according to the network diagram (hostnames, IP addresses, etc.)
    Remember to configure the gateway on the PCs.
    (You don't have to configure the switches)

- [ ] 2. Configure static routes on the routers to enable PC1 to successfully ping PC2.

### Task 1 - Configure all devices.

> Router 1
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
R1(config)#int g0/1
R1(config-if)#ip add 192.168.1.254 255.255.255.0
R1(config-if)#no shut

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up
int g0/0
R1(config-if)#ip add 192.168.12.1 255.255.255.0
R1(config-if)#no shut

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up

R1(config-if)#
```

> Router 2
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R2
R2(config)#int g0/0
R2(config-if)#ip add 192.168.12.2 255.255.255.0
R2(config-if)#no shut

R2(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up

R2(config-if)#int g0/1
R2(config-if)#ip add 192.168.13.2 255.255.255.0
R2(config-if)#no shut

R2(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up

R2(config-if)#
```

>Router 3
```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R3
R3(config)#int g0/0
R3(config-if)#ip add 192.168.13.3 255.255.255.0
R3(config-if)#no shut

R3(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0, changed state to up

R3(config-if)#int g0/1
R3(config-if)#ip add 192.168.3.254 255.255.255.0
R3(config-if)#no shut

R3(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up

R3(config-if)#
```
> PC Configuration
| Device | Address | Mask | Deafult Gateway |Connects to |
|:--|:--|:--|:--|
| PC1 | 192.168.1.1 | 255.255.255.0 | 192.168.1.254 | SW1 > R1 |
| PC2 | 192.168.3.1 | 255.255.255.0 | 192.168.3.254 | SW2 > R3 |

> Full Device Configuration
| Device | Address | Mask | Connects to |
|:--|:--|:--|:--|
| R1 (G0/0) | 192.168.12.1 | 255.255.255.0 | R2 |
| R1 (G0/1) | 192.168.1.254 | 255.255.255.0 | SW1 > PC1 |
| R2 (G0/0) | 192.168.12.2 | 255.255.255.0 | R1 |
| R2 (G0/1) | 192.168.13.2 | 255.255.255.0 | R3 |
| R3 (G0/0) | 192.168.13.3 | 255.255.255.0 | R2 |
| R3 (G0/1) | 192.168.3.254 | 255.255.255.0 | SW1 > PC2 |
| PC1 | 192.168.1.1 | 255.255.255.0 | SW1 > R1 |
| PC2 | 192.168.3.1 | 255.255.255.0 | SW2 > R3 |

### Task 2 - Configure router static routes

> Router 1
```
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#ip route 192.168.3.0 255.255.255.0 192.168.12.2
R1(config)#
```

> Router 2
```
R2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R2(config)#ip route 192.168.1.0 255.255.255.0 192.168.12.1
R2(config)#ip route 192.168.3.0 255.255.255.0 192.168.13.3
R2(config)#
```

> Router 3
```
R3#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R3(config)#ip route 192.168.1.0 255.255.255.0 192.168.13.2
R3(config)#
```

## Tests


## Evidence

evidence/config-static-routes/011-pt1-topology.drawio.png

evidence/config-static-routes/ping-confirmation.png

evidence/config-static-routes/router1_config.txt

evidence/config-static-routes/router2_config.txt

evidence/config-static-routes/router3_config.txt

## Key Takeaways

## Command Cheat Sheet

---



## Synopsis

Day 11 (Static Route Configuration) of Jeremy's IT Lab labs.

Getting more hands on into the CLI. A lot of information I have already knew still.

**Next:** Day 012 · IPv4 Addressing (part1) · **Previous:** Day 010 · Ethernet LAN Switching (part 1)
