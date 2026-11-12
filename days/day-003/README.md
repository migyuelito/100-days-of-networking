# Day 003 — The TCP/IP Model
<!-- Aim for 10 minutes of writing. Copy this file to days/day-NNN/README.md. -->

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-11 | 10 min | Jeremy's IT Lab, Free CCNA: Day 3 (The TCP/IP Model) and Day 3 Lab (OSI Model)  — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided · Rebuilt |

**Goal:** Reviewing the OSI model by analyzing traffic content of each payload.

## What I did

- [x] Guided: Followed lab instructions of sending and analysing traffic with Packet Tracer simulation mode.

## Topology

![Day 003 topology:](evidence/003-topology.drawio.png)

## What happened and why

Day 3 of Jeremy's IT Lab labs.

1 - Creating traffic on the client, releasing PC1's IP address.
    1a. Traffic is created with some destination information. Broadcast MAC of FFFF.FFFF.FFFF. Broadcast IP of 255.255.255.255. Port destination of 67 (DHCP Server)

2 - PDU is sent through the wire to SVR1.
    2a. SW2 and SW1 receive the PDU. Save the MAC address of PC1 to its MAC address table under the associated port(s). Then forward the PDU to all other ports due to it being a broadcast.


**Previous:** [Day 001 · Network Devices](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-001/README.md) | **Next:** Day 003 · **Intro to the CLI**
