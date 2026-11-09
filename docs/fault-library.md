# Fault library

Faults to plant when a day calls for "introduce a fault," and on review days. Each row says what you'll probably notice and where the evidence usually shows up.

**How to plant faults so the diagnosis is real**

1. Save a working copy of a lab, then plant one or two faults in a second copy.
2. Pick them at random (roll a die against the row numbers) so you don't know which one you chose, or ask someone else to plant them.
3. Wait at least a day before diagnosing. Write the symptom first, the way a user would report it.
4. Diagnose from symptoms and commands only, then record the trail with the troubleshooting table in your journal.

| # | Area | Fault to plant | What you'll probably notice | Where to look |
|---|---|---|---|---|
| 1 | Addressing | Wrong subnet mask on a host | Some destinations work and others don't | `ipconfig` against the addressing plan |
| 2 | Addressing | Wrong or missing default gateway | Same-subnet pings work; everything else fails | `ipconfig`, then ping the gateway |
| 3 | Interfaces | Router interface left shut down | Link light off or red; connected route missing | `show ip interface brief` |
| 4 | VLANs | Access port in the wrong VLAN | Host can't reach its gateway, or gets a lease from the wrong pool | `show vlan brief`, `show interfaces <port> switchport` |
| 5 | Trunking | VLAN missing from a trunk's allowed list | One VLAN fails across the link while others work | `show interfaces trunk` |
| 6 | Trunking | One side trunk, the other side access | Link is up but tagged VLANs don't pass | `show interfaces trunk`, `show interfaces <port> switchport` |
| 7 | Trunking | Native VLAN mismatch | Console mismatch messages; untagged traffic lands in the wrong VLAN | `show interfaces trunk`, console log |
| 8 | Router-on-a-stick | Subinterface tagged with the wrong VLAN number | That VLAN's hosts can't reach their gateway | `show running-config interface <subinterface>` |
| 9 | STP | Default priorities left in place (unplanned root) | Traffic takes an unexpected path | `show spanning-tree` |
| 10 | STP | BPDU guard on a port that receives BPDUs | Port goes err-disabled | `show interfaces status err-disabled` |
| 11 | EtherChannel | Mismatched modes (on with active, or passive with passive) | Channel doesn't form; links may run separately or block | `show etherchannel summary` |
| 12 | Static routing | Missing return route | Request reaches the far side; replies never come back | `show ip route` on every hop, `traceroute` |
| 13 | OSPF | Area mismatch on a link | No neighbor on that link | `show ip ospf neighbor`, `show ip ospf interface` |
| 14 | OSPF | Hello or dead timer mismatch | No neighbor on that link | `show ip ospf interface` |
| 15 | OSPF | `passive-interface` on a transit link | No neighbor; routes behind it disappear | `show ip protocols` |
| 16 | HSRP | Group number or virtual IP mismatch | Both routers claim active, or the gateway is unreachable | `show standby brief` |
| 17 | HSRP | Preempt missing | The original active router doesn't take over again after recovery | `show standby` |
| 18 | DHCP | `ip helper-address` missing on a remote subnet's gateway | Clients get 169.254.x.x | `show running-config interface <gateway interface>`, `show ip dhcp binding` |
| 19 | DHCP snooping | Uplink toward the DHCP server left untrusted | Clients get no lease | `show ip dhcp snooping` |
| 20 | Port security | Violation after a device swap | Port goes err-disabled | `show port-security interface <port>` |
| 21 | ACLs | Applied in the wrong direction or on the wrong interface | Traffic you meant to block gets through, or the reverse | `show ip interface <interface>`, `show access-lists` |
| 22 | ACLs | A broad permit above a specific deny | The deny line never matches | `show access-lists` match counts |
| 23 | ACLs | No permit at the end | Everything not explicitly allowed stops working | `show access-lists` match counts |
| 24 | NAT | Inside and outside swapped | No translations appear | `show ip nat translations`, `show ip nat statistics` |
| 25 | SSH | Missing domain name or RSA keys, or the wrong `transport input` | SSH connection refused | `show ip ssh`, `show running-config \| section line vty` |

Packet Tracer only supports the commands its developers built in. If a fault behaves differently from what you expect, note it in your journal; that observation is useful evidence in its own right.
