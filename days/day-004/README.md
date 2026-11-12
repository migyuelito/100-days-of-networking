# Day 004 — Intro to the CLI
<!-- Aim for 10 minutes of writing. Copy this file to days/day-NNN/README.md. -->

| Date | Time spent | Source | Work type |
|---|---|---|---|
| 2026-11-12 | 10 min | Jeremy's IT Lab, Free CCNA: Day 4 (Intro to the CLI) and Day 4 Lab (Device Security)  — [playlist](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) | Guided · Rebuilt |

**Goal:** Reviewing the OSI model by analyzing traffic content of each payload.

## What I did

- [x] Guided: Followed lab instructions of sending and analysing traffic with Packet Tracer simulation mode.

## Topology

![Day 004 topology:](evidence/004-topology.drawio.png)

### Tasks

- [x] 1. Change the hostnames of the router and switch to the appropriate names (R1, SW1)
            **My Solution:** Enter **configure terminal** and use the **hostname** command.

- [x] 2.  Configure an unencrypted enable password of 'CCNA' on both devices
            **My Solution:** In **configure terminal** use the **enable password** command and enter *CCNA*

- [x] 3. Exit back to user EXEC mode and test the password

- [x] 4.  View the password in the running configuration
            **My Solution:** Verified and confirmed password using **show running-config**

- [x] 5. Ensure that the current password, and all future passwords, are encrypted
            **My Solution:** In **configure terminal** use the **service password-encryption** command to encrypt current and future passwords.

- [x] 6. View the password in the running configuration

- [x] 7. Configure a more secure, encrypted enable password of 'Cisco' on both devices
            **My Solution:** In **configure terminal** use the **enable secret** command and enter *Cisco*

- [x] 8. Exit back to user EXEC mode and then return to privileged EXEC mode.
    Which password do you have to use?
            **My Solution:** Password being used would be the more secure *'Cisco'* password.

- [x] 9. View the passwords in the running configuration.
     What encryption type number is used for the encrypted 'enable password'?
            **My Solution:** Password encryption for *'enable password'* would be **Type 7**
     What encryption type number is used for the encrypted 'enable secret'?
            **My Solution:** Password encryption for *'enable secret'* would be **MD5**

- [x] 10. Save the running configuration to the startup configuration
            **My Solution:** Using **write memory** to save running-config to startup-config.

## Synopsis

Day 4 of Jeremy's IT Lab labs.

First true day of getting into the command line. A lot of the information I already knew a lot of.

**Previous:** [Day 003 · The TCP/IP Model](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-003/README.md) | **Next:** [Day 005 · Ethernet LAN Switching](https://github.com/migyuelito/100-days-of-networking/blob/main/days/day-005/README.md)
