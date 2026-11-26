# Day 012 — The Life of a Packet

<!-- Pre-drafted plan. Fill in every {{ }} with what you actually did and saw, tick the boxes you completed, and delete lines you didn't do. -->

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-25 | 13 min | Jeremy's IT Lab, Free CCNA: Day 12 (The Life of a Packet) and Day 12 Lab (The Life of a Packet) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | **Guided** |

**Goal:** Learn about how packets go accross networks.

## What I did

- [x] Guided: Followed the Day 6 lab instructions in Packet Tracer to test pings and Switch dynamically learining Mac addresses.

## Topology

evidence/006-topology.drawio.png

No default gateways; there's no router in this design.

| Host | Address | Mask |
|---|---|---|
| PC1 | 192.168.1.1 | 255.255.255.0 |
| PC2 | 192.168.1.2 | 255.255.255.0 |
| PC3 | 192.168.1.3 | 255.255.255.0 |
| PC4 | 192.168.1.4 | 255.255.255.0 |
## Lab Tasks

Both switches have an empty MAC address table, and all PCs have an empty ARP table.

- [x] 1. If PC1 pings to PC3, what messages will be sent over the network, 
     and which devices will receive them?
     **My Solution**: Since PC1 doesn't know the destination MAC for PC3 it will send an ARP Request with the destination of the IP address. This ARP Request will broadcast to every device connected to the SW1 and SW2 other than PC1 for SW1 and SW1 for SW2.

- [x] 2. Send the ping and use Packet Tracer's 'simulation mode' to verify your answer.

- [x] 3. Use pings to generate network traffic and allow the switches to learn the MAC addresses 
     of all PCs on the network.

- [x] 4. Use 'show' commands on the switches to identify the MAC address of each PC.

- [x] 5. Clear the dynamic MAC addresses from the MAC address table of each switch.

## Tests

| Test | Expected | Actual | Evidence |
|---|---|---|---|
| T1 · PC1 → PC2, same subnet | Replies (the first may time out while ARP resolves) | {{ACTUAL}} | [03](evidence/03-t1-ping-pc1-to-pc2.txt) |
| T2 · PC1 → PC3, different subnet | No replies: PC1 sees 192.168.2.10 as remote and has no gateway to send it to | {{ACTUAL}} | [04](evidence/04-t2-ping-pc1-to-pc3.txt) |
| T3 · Fault (PC2 at /16) · PC1 → PC2 | Still replies: each host still sees the other as local, so the fault hides | {{ACTUAL}} | [05](evidence/05-t3-ping-pc1-to-pc2-mask-fault.txt) |
| T4 · Fault (PC2 at /16) · PC2 → PC3 | No replies: even if the request reaches PC3, PC3 sees PC2 as remote and has no gateway for the reply | {{ACTUAL}} | [06](evidence/06-t4-ping-pc2-to-pc3-mask-fault.txt) · [07](evidence/07-t4-simulation-mode.png) |
| T5 · Fix · `ipconfig` on PC2 | Mask back to 255.255.255.0, matching the plan | {{ACTUAL}} | [08](evidence/08-t5-ipconfig-pc2-fixed.txt) |

## Evidence

SW1 CLI Output:
SW1>en
SW1#show mac-
SW1#show mac-address-table 
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0001.647b.3119    DYNAMIC     Gig0/1
   1    0004.9a6e.d870    DYNAMIC     Gig0/1
   1    00d0.d3ad.9cab    DYNAMIC     Fa0/1
SW1#show mac-address-table 
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0001.647b.3119    DYNAMIC     Gig0/1
   1    0004.9a6e.d870    DYNAMIC     Gig0/1
   1    0060.5c56.14d3    DYNAMIC     Fa0/2
   1    00d0.d3ad.9cab    DYNAMIC     Fa0/1
SW1#clear ma
SW1#clear mac-
SW1#clear mac-address-table dyna
SW1#clear mac-address-table dynamic 
SW1#show mac-address
SW1#show mac-address-table 
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

SW1#

SW2 CLI Output:
SW2>en
SW2#show mac-address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0001.647b.3119    DYNAMIC     Fa0/2
   1    0004.9a6e.d870    DYNAMIC     Fa0/1
   1    0060.5c56.14d3    DYNAMIC     Gig0/1
   1    00d0.d3ad.9cab    DYNAMIC     Gig0/1
SW2#
SW2#clear mac-
SW2#clear mac-address-table dynamic
SW2#clear mac-address-table dynamic 
SW2#show mac-address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

SW2#

## Key Takeaways

## Command Cheat Sheet

## Synopsis

Day 6 of Jeremy's IT Lab labs.

Getting more hands on into the CLI. A lot of information I have already knew still.

**Next:** Day 007 · IPv4 Addressing (part1) · **Previous:** Day 005 · Ethernet LAN Switching (part 1)
