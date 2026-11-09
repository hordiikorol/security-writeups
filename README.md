# Security Writeups — CTFs & Hands-On Labs

A running portfolio of my cybersecurity work: capture-the-flag challenge writeups and hands-on DFIR/blue-team lab investigations. Each writeup records the steps I actually took — including dead ends — so it is useful both as a learning log and as a portfolio. New CTFs are added under [`ctf/`](ctf/) as I play them.

## About me

I am a first-semester MSc Cybersecurity student at TalTech with a BSc in IT. My strongest areas are blue-team and SOC work: log analysis, alert triage, network traffic analysis, and Windows and Linux forensics. I hold CompTIA CySA+, Network+, and A+; AWS Cloud Practitioner; Linux Essentials; and ITIL certifications. I am actively developing my offensive-security skills (recon, enumeration, and exploitation).

**Tools:** Wireshark, Volatility, Autopsy, CyberChef, Ghidra, Splunk, Python, Bash, PowerShell, SQL.

## CTF writeups

### CSCTF 2026

A free online jeopardy-style CTF (Nov 2026).

| Challenge | Category | Status | Writeup |
|---|---|---|---|
| Operation Blackout | ICS | ✅ Solved | [writeup](ctf/csctf-2026/ics-operation-blackout/operation-blackout.md) |
| Velora | Web | ✅ Solved | [writeup](ctf/csctf-2026/web-velora/velora.md) |

## TryHackMe labs

Standalone DFIR / blue-team investigations, each written up in full with supporting screenshots.

| Lab | Focus | Write-up |
|---|---|---|
| Investigating Windows DFIR | Host-based Windows Server compromise analysis | [read](tryhackme/investigating-windows-dfir/) |
| DFIR — Windows & Splunk Investigations | Splunk log intrusion analysis | [read](tryhackme/dfir-windows-and-splunk-investigations/) |
| Volatility Memory Forensics | Memory forensics (banking trojan, WannaCry) | [read](tryhackme/volatility-memory-forensics/) |
| MirrorBlast C2 Triage | PCAP C2 triage (MirrorBlast / TA505) | [read](tryhackme/mirrorblast-c2-analysis/) |
| Endpoint Intrusion Analysis | Splunk/Sysmon endpoint intrusion | [read](tryhackme/splunk-endpoint-forensics/) |

## Repository layout

```
ctf/                     CTF writeups, grouped by event then challenge
  csctf-2026/
    ics-operation-blackout/   writeup + images + challenge-files
    web-velora/               writeup + images
tryhackme/               Standalone TryHackMe lab investigations
  <lab>/                      README (full write-up) + evidence/screenshots
```

Each CTF challenge folder keeps its screenshots in `images/` and (where provided) the original challenge artifacts in `challenge-files/`.
