<div align="center">
<a id="readme-top"></a>

# 🚀 Pre-Publication Checklist

**Run this before you make a repo public, and again before you share a link in a job application.**

</div>

## ⚡ Quick Commands

```bash
# No placeholders left (templates are meant to have them)
git grep -nIE "\{\{" -- ':(exclude)templates'

# Only your own work is tracked: no course .pkt or .pka files, flashcards, slides, or PDFs
git ls-files

# Secrets sweep: run before every push
git grep -n -i -E "password|secret|community|key-string|pre-shared|psk|token"
```

## ⏱️ Readability: The Two-Minute Scan

- [ ] The README opens with one sentence on what this is and who built it
- [ ] The featured projects table is current, and every Complete item links to evidence
- [ ] Each project summary fits on one screen and starts with the problem
- [ ] Diagrams show device names, interfaces, VLANs, and subnets
- [ ] Headings say what's in the section ("Guest isolation tests," not "Part 3")
- [ ] No placeholders left: `git grep -nIE "\{\{" -- ':(exclude)templates'` returns nothing
- [ ] Planned work is labeled Planned, and nothing implies a result you didn't observe

## 📜 Attribution

- [ ] Every guided day names its source and links to the lesson
- [ ] The work type says exactly what you did on your own
- [ ] No course files committed (lab `.pkt` or `.pka` files, flashcards, slides, PDFs): `git ls-files` lists only your own work
- [ ] Images or diagrams made by others are credited, or removed
- [ ] ATTRIBUTION.md is up to date

## 🔗 Links

- [ ] After pushing, click every link in the README on GitHub itself
- [ ] External links open the official page
- [ ] File names match their links exactly; GitHub paths are case-sensitive

## 🔐 Credentials and Secrets

- [ ] No real passwords anywhere. Lab passwords are obviously fake (for example `LabOnly-NotReal1`) and never reused elsewhere
- [ ] In configs, these are replaced with `<REDACTED>`: `enable secret`, `username … secret`, SNMP community strings, pre-shared keys, RADIUS and TACACS+ keys, Wi-Fi passphrases
- [ ] Hashes count as secrets too: Cisco type 7 passwords are reversible, and type 5, 8, and 9 hashes can be cracked offline
- [ ] No API tokens, VPN profiles, private keys, or `.env` files
- [ ] Before every push: `git grep -n -i -E "password|secret|community|key-string|pre-shared|psk|token"`
- [ ] Screenshots checked for passwords, tokens, email, and other open windows or tabs

## 🏠 Home Network Details (Home Lab Repo)

- [ ] Public IP address, ISP account details, and dynamic DNS names removed
- [ ] Real Wi-Fi network names (SSIDs) replaced with generic names
- [ ] MAC addresses, serial numbers, and asset tags removed
- [ ] Hostnames that reveal your name, family, or location replaced
- [ ] Remote access and open ports described in general terms only
- [ ] Photos don't show your address, windows, or labels, and phone photos have location data removed
- [ ] Private addresses are fine to show, but representative subnets are safer

## 🚨 If Something Sensitive Was Already Pushed

> [!CAUTION]
> 1. **Treat it as exposed.** Change the password, revoke the key or token, or rotate the passphrase first.
> 2. **Then remove it from history** (for example with `git filter-repo`) or recreate the repo. Deleting the file in a new commit isn't enough, because it stays in the history.

## 🎤 Explain-It Check

Answer each out loud in about two minutes, without notes. If you can't, the write-up isn't finished.

| # | Question | What to cover |
|:--:|:--|:--|
| 1 | **"Walk me through what you built."** | Problem, then design, then how you proved it. |
| 2 | **"Why this design and not another?"** | Name one alternative you considered and the tradeoff you accepted. |
| 3 | **"How do you know it works?"** | Point to one test: what you expected, what you saw, and where the evidence is. |
| 4 | **"What broke, and how did you find it?"** | Symptom, your first hypothesis, the command that proved or ruled it out, the fix, and the retest. |
| 5 | **"What would change in a production network?"** | Scale, hardware, change control, monitoring, and real failover timing. |
| 6 | **"Which parts did you do yourself?"** | Guided, rebuilt, changed, diagnosed, or original, without overstating it. |
| 7 | **"What could someone on the guest network still reach?"** | Name what your design still allows and how you'd close it. |

---

<div align="center">

⬅️ **[Back to README](../README.md)** &nbsp;&nbsp;•&nbsp;&nbsp; **[⬆ Back to top](#readme-top)**

</div>
