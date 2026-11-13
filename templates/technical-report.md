<div align="center">
<a id="readme-top"></a>

# 📘 {{PROJECT_TITLE}}: Technical Report

| | |
|:--|:--|
| 👤 **Author** | {{YOUR_NAME}} |
| 📅 **Dates** | {{YYYY-MM-DD}} to {{YYYY-MM-DD}} (Days {{X–Y}}) |
| 🖥️ **Platform** | {{e.g., Cisco Packet Tracer 9.0, or home lab hardware}} |
| 📊 **Status** | {{Planned · In progress · Complete}} |
| 🛠️ **Work type** | {{Original · Based on <source + link>, with these changes: …}} |
| 📄 **Summary page** | [README.md](README.md) |

</div>

<!-- For projects worth highlighting. Save as projects/<project-name>/report.md. Delete sections that don't apply, and their lines in the contents list. -->

<details>
<summary><b>📑 Contents</b></summary>

1. [Summary](#-1-summary)
2. [Problem and context](#-2-problem-and-context)
3. [Requirements](#-3-requirements)
4. [Topology](#-4-topology)
5. [Addressing and VLAN plan](#-5-addressing-and-vlan-plan)
6. [Traffic policy](#-6-traffic-policy)
7. [Key configuration choices](#-7-key-configuration-choices)
8. [Tradeoffs and alternatives](#-8-tradeoffs-and-alternatives)
9. [Verification](#-9-verification)
10. [Failure and outage tests](#-10-failure-and-outage-tests)
11. [Troubleshooting log](#-11-troubleshooting-log)
12. [Lessons learned](#-12-lessons-learned)
13. [Next steps](#-13-next-steps)
14. [Files and attribution](#-14-files-and-attribution)

</details>

## 📌 1. Summary

{{3–4 sentences: what you built, the key requirement, how you proved it, and the most important finding.}}

## 🧭 2. Problem and Context

{{Who needs what, and why. Keep it realistic, e.g., "A 25-person office needs guest access that can't reach internal systems."}}

## 📋 3. Requirements

Give each requirement an ID so every test can point back to it.

| ID | Requirement | Type |
|:--|:--|:--|
| R1 | {{e.g., Employees reach the file server}} | Functional |
| R2 | {{e.g., Guests reach the internet but no internal address}} | Security |
| R3 | {{e.g., One uplink failure doesn't cut users off}} | Availability |

**Scope and assumptions**

- **In scope:** {{ }}
- **Out of scope:** {{ }}
- **Assumptions:** {{ }}
- **Platform limits:** {{e.g., Packet Tracer doesn't model real-time convergence, so failover results compare replies lost rather than milliseconds}}

## 🌐 4. Topology

<p align="center">
  <img src="topology.png" alt="{{Topology diagram description}}">
</p>

| Device | Role | Key interfaces |
|:--|:--|:--|
| {{R1}} | {{Edge router, inter-VLAN routing}} | {{G0/0/0 to ISP, G0/0/1 trunk to SW1}} |

## 🔢 5. Addressing and VLAN Plan

| VLAN | Name | Subnet | Gateway | DHCP range | Notes |
|:--|:--|:--|:--|:--|:--|
| {{10}} | {{EMPLOYEES}} | {{ }} | {{ }} | {{ }} | {{ }} |

{{Show your sizing logic in one or two lines, e.g., "Guest: up to 50 devices, so /26 (62 usable)."}}

## 🚦 6. Traffic Policy

| From ↓ / To → | {{Zone A}} | {{Zone B}} | {{Management}} | {{Internet}} |
|:--|:--:|:--:|:--:|:--:|
| {{Zone A}} | — | {{ }} | {{ }} | {{ }} |
| {{Zone B}} | {{ }} | — | {{ }} | {{ }} |

<sub>✅ allowed · ❌ blocked · ⚠️ allowed with conditions (explain below the table)</sub>

## 🔧 7. Key Configuration Choices

### 7.1 {{Choice, e.g., Named extended ACL inbound on the guest subinterface}}

```
{{The essential lines only. Full configs live in configs/.}}
```

💡 **Why:** {{What requirement this meets, and why this placement or method.}}

## 🔀 8. Tradeoffs and Alternatives

| Decision | Alternatives considered | Why I chose it | What it costs |
|:--|:--|:--|:--|
| {{ }} | {{ }} | {{ }} | {{ }} |

## ✅ 9. Verification

| Test | Req | Method (command or action) | Expected | Actual | Evidence |
|:--|:--|:--|:--|:--|:--|
| T1 | R1 | {{ }} | {{ }} | {{ }} | [link](evidence/{{FILE}}) |
| T2 | R2 | {{ }} | {{ }} | {{ }} | [link](evidence/{{FILE}}) |

> [!NOTE]
> **Result:** {{X of Y tests matched expectations. Explain any mismatch in section 11.}}

## 💥 10. Failure and Outage Tests

| Test | What I broke | What I measured | Expected | Actual | Evidence |
|:--|:--|:--|:--|:--|:--|
| F1 | {{e.g., Shut the active uplink}} | {{e.g., Replies lost in a continuous ping; which gateway became active}} | {{ }} | {{ }} | [link](evidence/{{FILE}}) |

## 🔍 11. Troubleshooting Log

### Issue {{N}}: {{Symptom in plain words}}

- **Symptom:** {{What a user would report}}
- **Scope:** {{What's affected, and what still works}}

| Step | Hypothesis | Check (command) | Result | Verdict |
|:--:|:--|:--|:--|:--|
| 1 | {{ }} | `{{COMMAND}}` | {{ }} | {{Ruled out · Confirmed}} |

- **Root cause:** {{ }}
- **Fix:** {{Exact change}}
- **Retest:** {{Which tests you re-ran, including the ones that already passed}}
- **Prevention:** {{Checklist item or design change}}

## 🎓 12. Lessons Learned

- {{ }}

## 🔭 13. Next Steps

- {{ }}

## 📁 14. Files and Attribution

| File | Description | Created by |
|:--|:--|:--|
| `configs/{{DEVICE}}.txt` | {{Final running config}} | {{Me}} |

Sources: {{Course, documentation, or RFCs you used, with links}}

---

<div align="center">

📄 **[Summary page](README.md)** &nbsp;&nbsp;•&nbsp;&nbsp; **[⬆ Back to top](#readme-top)**

</div>
