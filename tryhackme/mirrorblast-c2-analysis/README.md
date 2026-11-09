# MirrorBlast C2 Triage

> TryHackMe · PCAP triage of a **Malware Command-and-Control** alert — confirmed True Positive, attributed to **MirrorBlast / TA505**. · Case `THM-WZ1-2026`

## Overview

A network-forensics triage of a high-priority "Malware Command and Control Activity" alert. Systematic PCAP analysis confirmed the alert as a **True Positive** and attributed the infection to the **MirrorBlast** malware family, a tool associated with threat actor **TA505** (aka Hive0065 / Graceful Spider).

## Tools

Brim (log aggregation / signature ID), Wireshark (deep packet inspection), VirusTotal (threat intel + attribution), CyberChef (IOC defanging).

## Key findings

- **Alert signature:** `ET MALWARE MirrorBlast CnC Activity M3`.
- **Infected host:** `172.16.1.102` → **C2** `169.239.128.11`.
- **Attribution:** TA505 — MirrorBlast, delivered via Windows Installer (`.msi`) over HTTP.
- **C2 fingerprint:** User-Agent `REBOL View 2.7.8.3.1`; HTTP GET with encoded parameters.
- **Redundant infrastructure:** secondary endpoints `185.10.68.235`, `192.36.27.92`.
- **Initial stagers:** `filter.msi`, `10opd3r_load.msi`.
- **Persistence artifacts:** `C:\ProgramData\001\` (`arab.bin`, `arab.exe`) and `C:\ProgramData\Local\Google\` (`rebol-view-278-3-1.exe`, `exemple.rb`).

## Indicators of compromise

| Type | Indicator |
|---|---|
| Infected host | `172.16.1.102` |
| C2 IP | `169.239.128.11` |
| Secondary IPs | `185.10.68.235`, `192.36.27.92` |
| User-Agent | `REBOL View 2.7.8.3.1` |
| Stagers | `filter.msi`, `10opd3r_load.msi` |
| Dropped files | `arab.exe`, `arab.bin`, `rebol-view-278-3-1.exe`, `exemple.rb` |

## Full report

📄 [mirrorblast-c2-triage.docx](report/mirrorblast-c2-triage.docx)

---

*Analyst: Hordii Korol. Skills: PCAP analysis, IDS signature triage, threat-intel attribution, IOC extraction. Originally published at `github.com/hordiikorol/MirrorBlast-C2-Analysis`.*
