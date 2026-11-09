# Security Writeups — CTFs & Hands-On Labs

A running portfolio of my cybersecurity work: capture-the-flag challenge writeups and hands-on DFIR/blue-team lab investigations. Each writeup records the steps I actually took — including dead ends — so it is useful both as a learning log and as a portfolio. New CTFs are added under [`ctf/`](ctf/) as I play them.

## About me

I am a first-semester MSc Cybersecurity student at TalTech with a BSc in IT. My strongest areas are blue-team and SOC work: log analysis, alert triage, network traffic analysis, and Windows and Linux forensics. I hold CompTIA CySA+, Network+, and A+; AWS Cloud Practitioner; Linux Essentials; and ITIL certifications. I am actively developing my offensive-security skills (recon, enumeration, and exploitation).

**Tools:** Wireshark, Volatility, Autopsy, CyberChef, Ghidra, Splunk, Python, Bash, PowerShell, SQL.

## CTF writeups

### CSCTF 2026

A free online jeopardy-style CTF (Nov 2026).

| Challenge | Category | Points | Status | Writeup |
|---|---|---:|---|---|
| Operation Blackout | ICS | 708 | ✅ Solved | [writeup](ctf/csctf-2026/ics-operation-blackout/operation-blackout.md) |
| Velora | Web | 900 | 🚧 In progress | [writeup](ctf/csctf-2026/web-velora/velora.md) |

## TryHackMe labs

Standalone DFIR / blue-team investigations, each with a full report and supporting evidence.

| Lab | Focus | Report |
|---|---|---|
| [Investigating Windows DFIR](tryhackme/investigating-windows-dfir/) | Host-based Windows Server compromise analysis | [PDF](tryhackme/investigating-windows-dfir/report/windows_host_compromise_analysis.pdf) |
| [DFIR — Windows & Splunk Investigations](tryhackme/dfir-windows-and-splunk-investigations/) | Splunk log intrusion analysis | [PDF](tryhackme/dfir-windows-and-splunk-investigations/report/splunk_log_intrusion_analysis.pdf) |
| [Volatility Memory Forensics](tryhackme/volatility-memory-forensics/) | Memory forensics (banking trojan, WannaCry) | [PDF](tryhackme/volatility-memory-forensics/report/Volatility_Memory_Forensics_Report.dpf.pdf) |
| [MirrorBlast C2 Analysis](tryhackme/mirrorblast-c2-analysis/) | C2 traffic / incident analysis | [DOCX](tryhackme/mirrorblast-c2-analysis/Incident%20Analysis%20Report.docx) |
| [Splunk Endpoint Forensics](tryhackme/splunk-endpoint-forensics/) | Endpoint forensics with Splunk | [DOCX](tryhackme/splunk-endpoint-forensics/Incident%20Analysis%20Report.docx) |

## Repository layout

```
ctf/                     CTF writeups, grouped by event then challenge
  csctf-2026/
    ics-operation-blackout/   writeup + images + challenge-files
    web-velora/               writeup + images
tryhackme/               Standalone TryHackMe lab investigations
  <lab>/                      README + report + evidence/screenshots
```

Each CTF challenge folder keeps its screenshots in `images/` and (where provided) the original challenge artifacts in `challenge-files/`.
