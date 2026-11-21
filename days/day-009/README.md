# Day 009 — Switch Interfaces

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-21 | 15 min | Jeremy's IT Lab, Free CCNA: Day 9 (Switch Interfaces) and Day 9 Lab (Configuring Interfaces) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided |

**Goal:** Set up Packet Tracer, rebuild the Day 1 topology from memory, and prove where a subnet boundary stops traffic, even on a single switch.21

## What I did

- [ ] Guided: followed the Day 1 Lab
- [ ] Rebuilt the topology from a blank file, without the video
- [ ] Changed a requirement: PC3 on its own subnet (192.168.2.0/24), same switch
- [ ] Planted and diagnosed a fault: PC2's mask set to 255.255.0.0

## Topology

"evidence/009-topology.drawio.png"

| Host | Address | Mask |
|---|---|---|
| PC1 | 192.168.1.10 | 255.255.255.0 |
| PC2 | 192.168.1.20 | 255.255.255.0 |
| PC3 | 192.168.2.10 | 255.255.255.0 |

## Lab Tasks

- [ ] 1. Configure the hostname of R1, SW1, and SW2

- [ ] 2. Configure the appropriate IP addresses on R1, PC1, PC2, PC3, PC4

- [ ] 3. Manually configure the speed and duplex on interfaces connected to other 
    networking devices (not end hosts)

- [ ] 4. Configure appropriate descriptions on each interface

- [ ] 5. Disable interfaces which are not connected to other devices

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

### Task 4

### Task 5

## What happened and why

{{2–4 sentences. Cover why one switch can't connect two subnets on its own, why the mask fault passed T3, and what Simulation mode showed for T4.}}

## Remember next time

- `ipconfig` — check it against the addressing plan before trusting a ping
- Simulation mode — shows where a packet stops and why

**Next:** Day 010 · **Re-run from memory on:** Day 008
