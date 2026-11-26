<div align="center">
<a id="readme-top"></a>

# 💻 Day 012 — The Life of a Packet

**A review day: how one ping crosses the network, hop by hop**

[![Day](https://img.shields.io/badge/Day-012_%2F_100-0D274D?style=for-the-badge)](https://github.com/migyuelito/100-days-of-networking)
![Topic](https://img.shields.io/badge/Topic-Life_of_a_Packet-049FD9?style=for-the-badge)
![Type](https://img.shields.io/badge/Type-Review_Day-2EA44F?style=for-the-badge)

| 📅 Date | ⏱️ Time spent | 📚 Source | 🛠️ Work type |
|---|---|---|---|
| 2026-11-25 | 13 min | Jeremy's IT Lab, Free CCNA<br>Day 12 (The Life of a Packet)<br>Day 12 Lab (Life of a Packet)<br>▶️ [Playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided |

</div>

> 🎯 **Goal:** Learn how packets travel across networks.

## 📋 What I Did

- [x] **Guided:** Used Day 12 as a review day: went through the Life of a Packet lab, which walks a packet across the network, and revisited my previous labs.

## 🔁 Review: One Ping, Hop by Hop

PC1 pinging PC2 across the three routers from [Day 11's lab](../day-011/README.md):

| Hop | Source MAC 🔄 | Destination MAC 🔄 | Source → destination IP 🔒 | TTL |
|:--|:--|:--|:--|:--:|
| PC1 → R1 | PC1 | R1 G0/1 | 192.168.1.1 → 192.168.3.1 | 128 |
| R1 → R2 | R1 G0/0 | R2 G0/0 | 192.168.1.1 → 192.168.3.1 | 127 |
| R2 → R3 | R2 G0/1 | R3 G0/0 | 192.168.1.1 → 192.168.3.1 | 126 |
| R3 → PC2 | R3 G0/1 | PC2 | 192.168.1.1 → 192.168.3.1 | 125 |

<sub>🔄 rewritten at every hop · 🔒 the same end to end</sub>

- **Routers rebuild the frame, not the packet:** each one strips the Ethernet header, looks up the destination IP in its routing table, subtracts 1 from the TTL, and wraps the packet in a new frame for the next hop.
- **ARP finds each next hop's MAC:** the first time through, every device has to ask, which is why Day 11's first ping lost three packets, one per router.
- **Switches pass frames along untouched:** SW1 and SW2 forward by destination MAC without changing anything.

## 📝 Synopsis

***Day 12 of Jeremy's IT Lab.***

A bit of a freebie day: I used it to review how packets move through a network and to go back over my previous labs.

---

<div align="center">

⬅️ **Previous:** [Day 011 · Routing Fundamentals & Static Routing](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-011/README.md) &nbsp;&nbsp;•&nbsp;&nbsp; **Next:** Day 013 · Subnetting, Part 1 ➡️

**[⬆ Back to top](#readme-top)**

</div>
