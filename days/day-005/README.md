<div align="center">
<a id="readme-top"></a>

# 💻 Day 005 — Ethernet LAN Switching, Part 1

**A switch next to a hub: watching frames get learned, flooded, forwarded, and repeated**

[![Day](https://img.shields.io/badge/Day-005_%2F_100-0D274D?style=for-the-badge)](https://github.com/migyuelito/100-days-of-networking)
![Topic](https://img.shields.io/badge/Topic-Ethernet_Switching-049FD9?style=for-the-badge)
![Packet Tracer](https://img.shields.io/badge/Packet_Tracer-Simulation_Mode-2EA44F?style=for-the-badge)

| 📅 Date | ⏱️ Time spent | 📚 Source | 🛠️ Work type |
|---|---|---|---|
| {{YYYY-MM-DD}} | {{TIME}} | Jeremy's IT Lab, Free CCNA<br>Day 5 (Ethernet LAN Switching pt. 1)<br>Custom lab written with Claude (the course has no Day 5 lab)<br>▶️ [Playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided |

</div>

<!-- Aim for 10 minutes of writing. Copy this file to days/day-NNN/README.md. -->
<!-- Pre-drafted lab: replace each double-curly-brace placeholder with what you did and saw, tick the tasks you finish, and delete anything you skip. -->

> 🎯 **Goal:** Watch a switch learn, flood, and forward frames next to a hub that just repeats them, and read the fields of an Ethernet frame.

## 📋 What I Did

- [ ] **Guided:** Built the custom Day 5 lab in Packet Tracer and worked through its tasks in Simulation mode.

## 🗺️ Topology

<p align="center">
  <img src="evidence/005-topology.drawio.png" alt="Day 005 topology: PC1 and PC2 connect to SW1 on F0/1 and F0/2; SW1 F0/3 connects to a hub with a crossover cable; PC3 and PC4 connect to the hub. All hosts are in 192.168.5.0/24.">
</p>

No default gateways; there's no router in this design.

| Host | Address | Mask | Connects to |
|:--|:--|:--|:--|
| PC1 | 192.168.5.1 | 255.255.255.0 | SW1 F0/1 |
| PC2 | 192.168.5.2 | 255.255.255.0 | SW1 F0/2 |
| PC3 | 192.168.5.3 | 255.255.255.0 | HUB1 (any port) |
| PC4 | 192.168.5.4 | 255.255.255.0 | HUB1 (any port) |

SW1 F0/3 connects to HUB1.

> [!TIP]
> **Why a hub?** Hubs are obsolete, and that's the point. This is the Day 6 topology with SW2 swapped for a hub. A hub repeats every frame out every port; a switch learns where each device is and sends a frame only where it needs to go. Side by side, the switch's decisions are easy to see.

## 🧭 How a Switch Decides

Every frame that reaches SW1 goes through the same steps. HUB1 skips all of them and repeats the frame out every other port.

```mermaid
flowchart LR
    A([Frame arrives<br/>on a port]) --> B[Learn: map the source<br/>MAC to that port]
    B --> C{Destination<br/>FFFF.FFFF.FFFF?}
    C -- Yes --> F[Flood out every port<br/>except the one it came in on]
    C -- No --> D{Destination MAC<br/>in the MAC table?}
    D -- Yes --> E[Forward out<br/>that one port]
    D -- No --> F

    classDef step fill:#E8F4FD,stroke:#049FD9,stroke-width:2px,color:#0D274D
    classDef ask fill:#FFF4E5,stroke:#F59E0B,stroke-width:2px,color:#7C4A03
    classDef act fill:#EAF7EE,stroke:#2EA44F,stroke-width:2px,color:#14532D
    class A,B step
    class C,D ask
    class E,F act
```

## ✅ Lab Tasks

- [ ] [**Task 1**](#task-1--build-and-cable-the-topology) — Build and cable the topology
- [ ] [**Task 2**](#task-2--configure-sw1-and-address-the-pcs) — Configure SW1 the Day 4 way and address the PCs
- [ ] [**Task 3**](#task-3--record-each-pcs-mac-address) — Record each PC's MAC address
- [ ] [**Task 4**](#task-4--send-a-frame-through-the-hub) — Send a frame through the hub
- [ ] [**Task 5**](#task-5--watch-sw1-learn-and-flood) — Watch SW1 learn and flood
- [ ] [**Task 6**](#task-6--follow-the-reply-back-through-the-hub) — Follow the reply back through the hub
- [ ] [**Task 7**](#task-7--read-the-ethernet-frame) — Read the fields of an Ethernet frame
- [ ] [**Task 8**](#task-8--find-the-port-with-two-mac-addresses) — Find the switch port with two MAC addresses
- [ ] [**Task 9**](#task-9--flood-an-unknown-unicast-frame) — Clear SW1's MAC table and flood an unknown unicast frame
- [ ] [**Task 10**](#task-10--bonus-let-the-mac-table-age-out) — Bonus: let the MAC table age out

## 🔌 Part 1 — Build the LAN

### Task 1 — Build and cable the topology

> Add one **2960** switch, one **hub**, and four **PC-PT** PCs, rename them to match the topology, and cable them as shown.

🛠️ **In Packet Tracer:**
- **Switch:** Network Devices → Switches → **2960**. **Hub:** Network Devices → Hubs → **Hub-PT**. **PCs:** End Devices → **PC**.
- **Rename:** click a device → **Config** → **Display Name**.
- **Cables:** Connections → **Copper Straight-Through** for the PCs, **Copper Cross-Over** from SW1 F0/3 to the hub.
- Wait for SW1's link lights to turn green (about 30 seconds; that delay is Spanning Tree, a later topic).

💡 **My solution:** {{ }}

> [!NOTE]
> **Why does SW1 connect to the hub with a crossover cable?**
>
> ➜ {{your answer}}

### Task 2 — Configure SW1 and address the PCs

> Set SW1's hostname, protect privileged EXEC mode with an `enable secret`, and save the configuration. Then give each PC its address from the table (no default gateway).

```
Switch> enable
Switch# configure terminal
Switch(config)# hostname SW1
SW1(config)# enable secret LabOnly-NotReal1
SW1(config)# end
SW1# write memory
```

🛠️ **PC addresses:** click the PC → **Desktop** → **IP Configuration** → **Static**.

💡 **My solution:** {{ }}

### Task 3 — Record each PC's MAC address

> Find each PC's MAC address, fill in the table, and pick out the OUI.

🛠️ Click the PC → **Desktop** → **Command Prompt** → `ipconfig /all`, and read **Physical Address**.

| PC | MAC address | OUI (first 6 hex digits) |
|:--|:--|:--|
| PC1 | 00D0.58A1.5E10 | 00D0.58 |
| PC2 | 00D0.D35A.A031 | 00D0.D3 |
| PC3 | 0090.0C11.A512 | 0090.0C |
| PC4 | 0090.2BB5.9D79 | 0090.2B |

> [!NOTE]
> **What does the OUI identify, and how would Windows write PC1's MAC address (`xx-xx-xx-xx-xx-xx`)?**
>
> ➜ {{your answer}}

## ⚖️ Part 2 — Switch vs. Hub

### Task 4 — Send a frame through the hub

> Switch to Simulation mode and send one ping from PC3 to PC1. Step through the first frame until it leaves HUB1.

🛠️ **In Packet Tracer:**
1. Pick the **Inspect** tool (magnifying glass), click **SW1**, and choose **MAC Table**. Leave the window open; it updates live and should be empty.
2. Click **Simulation** (bottom right). Click **Edit Filters** and leave only **ARP** and **ICMP** checked.
3. Pick **Add Simple PDU** (closed envelope), click **PC3**, then **PC1**.
4. Press **Capture/Forward** (▶|) one step at a time. Click an envelope to open it; the **OSI Model** tab shows which layers that device used.

> [!TIP]
> The first frame isn't the ping. It's PC3's **ARP request** (Day 6), a broadcast asking for PC1's MAC address.

> [!NOTE]
> **What did HUB1 do with the frame, and which OSI layer did it work at? (Check HUB1's OSI Model tab.)**
>
> ➜ {{your answer}}
>
> **Try the Inspect tool on HUB1. Does it have a MAC table? Why or why not?**
>
> ➜ {{your answer}}

### Task 5 — Watch SW1 learn and flood

> Keep stepping until the frame leaves SW1.

> [!NOTE]
> **What did SW1 add to its MAC table, and which ports did it send the frame out of?**
>
> ➜ {{your answer}}
>
> **Compare SW1's OSI Model tab with HUB1's. Which extra layer does the switch use, and what does it use it for?**
>
> ➜ {{your answer}}

### Task 6 — Follow the reply back through the hub

> Step through PC1's ARP reply and the ping (ICMP echo request and reply) until the ping completes.

> [!NOTE]
> **SW1 sent PC1's reply out only one port, yet PC4 still received it. Why?**
>
> ➜ {{your answer}}
>
> **Did PC2 receive the ICMP echo request? Why or why not?**
>
> ➜ {{your answer}}

## 🔍 Part 3 — Anatomy of an Ethernet Frame

### Task 7 — Read the Ethernet frame

> In the **Event List**, click the first ARP event at PC3, then the first ICMP event at PC3. On **Outbound PDU Details**, find the **Ethernet II** header and fill in the table.

| Field | ARP frame | ICMP frame |
|:--|:--|:--|
| Destination MAC | {{ }} | {{ }} |
| Source MAC | {{ }} | {{ }} |
| Type | {{ }} | {{ }} |

> [!NOTE]
> **What do the two Type values tell the receiver?**
>
> ➜ {{your answer}}
>
> **An ARP message is 28 bytes, but an Ethernet payload must be at least 46 bytes. How many bytes of padding does the ARP frame need, and how big is the whole frame (header + payload + trailer)?**
>
> ➜ {{your answer}}

## 🔗 Part 4 — Many MACs, One Port

### Task 8 — Find the port with two MAC addresses

> Switch back to **Realtime** mode, ping PC2 from PC4, then check SW1's MAC table in the CLI. Copy the output into `evidence/03-sw1-mac-table.txt`.

```
C:\> ping 192.168.5.2                ← from PC4's Command Prompt
SW1# show mac address-table
```

> [!NOTE]
> **How many MAC addresses does SW1 list on F0/3, and why can one switch port have more than one?**
>
> ➜ {{your answer}}

## 🌊 Part 5 — Unknown Unicast Flooding

### Task 9 — Flood an unknown unicast frame

> Empty SW1's MAC table while PC1 still remembers PC4's MAC address, then ping PC4 from PC1 in Simulation mode.

🛠️ Do these three steps back to back:
1. In **Realtime** mode, ping PC4 from PC1: `ping 192.168.5.4`. This refreshes PC1's memory of PC4's MAC address.
2. On SW1, clear the learned addresses: `SW1# clear mac address-table dynamic`
3. Switch to **Simulation**, send a **Simple PDU** from PC1 to PC4, and step through it.

If an ARP request shows up first, PC1 had already forgotten PC4's MAC address. Repeat the three steps a little faster.

> [!NOTE]
> **There's no ARP request this time. Why not?**
>
> ➜ {{your answer}}
>
> **What does SW1 do with the echo request, and why? Which PCs receive a copy?**
>
> ➜ {{your answer}}
>
> **How is this flood different from the ARP broadcast in Task 5?**
>
> ➜ {{your answer}}

## ⏳ Bonus — MAC Aging

### Task 10 — Bonus: let the MAC table age out

> In Realtime mode, ping between a few PCs, leave everything idle for at least 5 minutes, then run `show mac address-table` on SW1 again. Copy the output into `evidence/05-sw1-mac-table-aged.txt`.

> [!NOTE]
> **What happened to the entries, and why?**
>
> ➜ {{your answer}}

## 🧪 Tests

<!-- Write each Expected before you run the test. Start each Actual with ✅ (matched) or ❌ (didn't match). -->

| Test | Expected | Actual | Evidence |
|:--|:--|:--|:--|
| T1 · Where HUB1 and SW1 send PC3's ARP request | {{your prediction}} | {{ }} | [01](evidence/01-arp-request-hub-and-switch.png) |
| T2 · Which PCs receive PC1's reply to PC3 | {{your prediction}} | {{ }} | [02](evidence/02-reply-through-hub.png) |
| T3 · SW1's MAC table after PC4 pings PC2 | {{your prediction}} | {{ }} | [03](evidence/03-sw1-mac-table.txt) |
| T4 · Where SW1 sends PC1's echo request after its table is cleared | {{your prediction}} | {{ }} | [04](evidence/04-unknown-unicast-flood.png) |
| T5 · SW1's MAC table after 5 minutes idle (bonus) | {{your prediction}} | {{ }} | [05](evidence/05-sw1-mac-table-aged.txt) |

## 📁 Evidence

<!-- Save screenshots and CLI output in evidence/ with these names so the links work. -->

| # | File | What it shows |
|:--:|:--|:--|
| 01 | [01-arp-request-hub-and-switch.png](evidence/01-arp-request-hub-and-switch.png) | Simulation: HUB1 repeats PC3's ARP request and SW1 floods it |
| 02 | [02-reply-through-hub.png](evidence/02-reply-through-hub.png) | Simulation: PC1's reply reaches PC4 through the hub |
| 03 | [03-sw1-mac-table.txt](evidence/03-sw1-mac-table.txt) | `show mac address-table`: two MAC addresses on F0/3 |
| 04 | [04-unknown-unicast-flood.png](evidence/04-unknown-unicast-flood.png) | Simulation: SW1 floods an unknown unicast frame |
| 05 | [05-sw1-mac-table-aged.txt](evidence/05-sw1-mac-table-aged.txt) | `show mac address-table` after 5 minutes idle (bonus) |

## 🧠 Key Takeaways

### Switch vs. hub

| | 🔁 Hub | 🔀 Switch |
|:--|:--|:--|
| **OSI layer** | Layer 1: repeats bits | Layer 2: reads frames and MAC addresses |
| **Learns MAC addresses** | No | Yes, from each frame's source MAC |
| **Broadcast frame** | Repeats out every other port | Floods out every other port |
| **Unknown unicast** | Repeats out every other port | Floods out every other port |
| **Known unicast** | Repeats out every other port | Forwards out one port |
| **Collision domain** | All ports share one | Each port is its own |

### The Ethernet frame

| Preamble | SFD | Destination | Source | Type | Payload | FCS |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
| 7 bytes | 1 byte | 6 bytes | 6 bytes | 2 bytes | 46–1500 bytes | 4 bytes |
| Clock sync | Start of frame | Receiver's MAC | Sender's MAC | What's inside | Packet + padding | Error check |

- **Header and trailer:** 14 bytes of header (destination, source, type) plus a 4-byte FCS trailer make 18 bytes. The preamble and SFD aren't counted.
- **Minimum frame:** 64 bytes, so payloads under 46 bytes get padded.
- **Type or length:** a value of 0x0600 (1536) or more is a type, like 0x0800 for IPv4 or 0x0806 for ARP. A value of 1500 or less is the payload length.
- **MAC addresses:** 48 bits, written as 12 hex digits. The first 6 digits are the OUI (the manufacturer), and the rest identify the device. `FFFF.FFFF.FFFF` is the broadcast address.
- **Aging:** a switch removes a dynamic MAC address after 5 minutes without frames from it.

## 📚 Command Cheat Sheet

| Command or tool | Where | What it does |
|:--|:--|:--|
| `enable secret LabOnly-NotReal1` | Global config | Sets a hashed enable password (Day 4) |
| `write memory` | Privileged EXEC | Saves the running config (Day 4) |
| `ipconfig /all` | PC → Command Prompt | Shows the PC's MAC address |
| `ping 192.168.5.4` | PC → Command Prompt | Sends ICMP echo requests |
| `show mac address-table` | Switch, privileged EXEC | Lists learned MACs and their ports |
| `clear mac address-table dynamic` | Switch, privileged EXEC | Removes all dynamically learned MACs |
| **Inspect** → **MAC Table** | Packet Tracer toolbar | Live view of a switch's MAC table |
| **Add Simple PDU** | Packet Tracer toolbar | Sends one ping between two devices |
| **Capture/Forward** | Simulation panel | Steps the simulation forward |

## 📝 Synopsis

{{2–4 sentences in your own words. The "why" is the part interviews ask about.}}

---

<div align="center">

⬅️ **Previous:** [Day 004 · Intro to the CLI](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-004/README.md) &nbsp;&nbsp;•&nbsp;&nbsp; **Next:** [Day 006 · Ethernet LAN Switching, Part 2](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-006/README.md) ➡️

**[⬆ Back to top](#readme-top)**

</div>
