# Day 001 — Packet Tracer setup and the subnet boundary

<!-- Pre-drafted plan. Fill in every {{ }} with what you actually did and saw, tick the boxes you completed, and delete lines you didn't do. -->

| Date | Time spent | Source | Work type |
|---|---|---|---|
| {{YYYY-MM-DD}} | {{TIME}} | Jeremy's IT Lab, Free CCNA: Day 1 (Network Devices) and Day 1 Lab (Packet Tracer Introduction) — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | {{Guided · Rebuilt · Changed · Diagnosed}} |

**Goal:** Set up Packet Tracer, rebuild the Day 1 topology from memory, and prove where a subnet boundary stops traffic, even on a single switch.

## What I did

- [ ] Guided: followed the Day 1 Lab
- [ ] Rebuilt the topology from a blank file, without the video → `day-001-rebuild.pkt`
- [ ] Changed a requirement: PC3 on its own subnet (192.168.2.0/24), same switch
- [ ] Planted and diagnosed a fault: PC2's mask set to 255.255.0.0

## Addressing

No default gateways yet; there's no router in this design.

| Host | Address | Mask |
|---|---|---|
| PC1 | 192.168.1.10 | 255.255.255.0 |
| PC2 | 192.168.1.20 | 255.255.255.0 |
| PC3 | 192.168.2.10 | 255.255.255.0 |

## Tests

| Test | Expected | Actual | Evidence |
|---|---|---|---|
| T1 · PC1 → PC2, same subnet | Replies (the first may time out while ARP resolves) | {{ACTUAL}} | [03](evidence/03-t1-ping-pc1-to-pc2.txt) |
| T2 · PC1 → PC3, different subnet | No replies: PC1 sees 192.168.2.10 as remote and has no gateway to send it to | {{ACTUAL}} | [04](evidence/04-t2-ping-pc1-to-pc3.txt) |
| T3 · Fault (PC2 at /16) · PC1 → PC2 | Still replies: each host still sees the other as local, so the fault hides | {{ACTUAL}} | [05](evidence/05-t3-ping-pc1-to-pc2-mask-fault.txt) |
| T4 · Fault (PC2 at /16) · PC2 → PC3 | No replies: even if the request reaches PC3, PC3 sees PC2 as remote and has no gateway for the reply | {{ACTUAL}} | [06](evidence/06-t4-ping-pc2-to-pc3-mask-fault.txt) · [07](evidence/07-t4-simulation-mode.png) |
| T5 · Fix · `ipconfig` on PC2 | Mask back to 255.255.255.0, matching the plan | {{ACTUAL}} | [08](evidence/08-t5-ipconfig-pc2-fixed.txt) |

## What happened and why

{{2–4 sentences. Cover why one switch can't connect two subnets on its own, why the mask fault passed T3, and what Simulation mode showed for T4.}}

## Remember next time

- `ipconfig` — check it against the addressing plan before trusting a ping
- Simulation mode — shows where a packet stops and why

**Next:** Day 002 · **Re-run from memory on:** Day {{NNN}}
