<div align="center">
<a id="readme-top"></a>

# 💻 Day 003 — The TCP/IP Model

**Following a broadcast through the OSI layers in Packet Tracer's simulation mode**

[![Day](https://img.shields.io/badge/Day-003_%2F_100-0D274D?style=for-the-badge)](https://github.com/migyuelito/100-days-of-networking)
![Topic](https://img.shields.io/badge/Topic-OSI_%26_TCP%2FIP-049FD9?style=for-the-badge)
![Packet Tracer](https://img.shields.io/badge/Packet_Tracer-Simulation_Mode-2EA44F?style=for-the-badge)

| 📅 Date | ⏱️ Time spent | 📚 Source | 🛠️ Work type |
|---|---|---|---|
| 2026-11-11 | 10 min | Jeremy's IT Lab, Free CCNA<br>Day 3 (The TCP/IP Model)<br>Day 3 Lab (OSI Model)<br>▶️ [Playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided · Rebuilt |

</div>

<!-- Aim for 10 minutes of writing. Copy this file to days/day-NNN/README.md. -->

> 🎯 **Goal:** Reviewing the OSI model by analyzing traffic content of each payload.

## 📋 What I Did

- [x] **Guided:** Followed lab instructions of sending and analysing traffic with Packet Tracer simulation mode.

## 🗺️ Topology

<p align="center">
  <img src="evidence/003-topology.drawio.png" alt="Day 003 topology: PC1 connects to SW2, SW2 connects to SW1, and SW1 connects to SVR1 and R1, which connects to R2">
</p>

## 💡 What Happened and Why

Day 3 of Jeremy's IT Lab labs.

### Step 1 — Creating traffic on the client, releasing PC1's IP address

Traffic is created with some destination information:

| OSI layer | Field | Value | Meaning |
|:--|:--|:--|:--|
| 2 · Data link | Destination MAC | `FFFF.FFFF.FFFF` | Broadcast: every device on the LAN |
| 3 · Network | Destination IP | `255.255.255.255` | Broadcast: every host on the local network |
| 4 · Transport | Destination port | `67` | DHCP server |

### Step 2 — PDU is sent through the wire to SVR1

SW2 and SW1 receive the PDU. Each one saves PC1's MAC address to its MAC address table under the associated port, then forwards the PDU to all other ports due to it being a broadcast.

```mermaid
sequenceDiagram
    participant PC1
    participant SW2
    participant SW1
    participant SVR1
    participant R1
    PC1->>SW2: Broadcast PDU (destination port 67)
    Note over SW2: Learns PC1's MAC, floods all other ports
    SW2->>SW1: Flooded
    Note over SW1: Learns PC1's MAC, floods all other ports
    SW1->>SVR1: Reaches the DHCP server
    SW1->>R1: Flooded
```

---

<div align="center">

⬅️ **Previous:** [Day 002 · Interfaces and Cables](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-002/README.md) &nbsp;&nbsp;•&nbsp;&nbsp; **Next:** [Day 004 · Intro to the CLI](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-004/README.md) ➡️

**[⬆ Back to top](#readme-top)**

</div>
