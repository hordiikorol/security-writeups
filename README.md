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
| [Volatility Memory Forensics](tryhackme/volatility-memory-forensics/) | Memory forensics (banking trojan, WannaCry) | [PDF](tryhackme/volatility-memory-forensics/report/volatility_memory_forensics_report.pdf) |
| [MirrorBlast C2 Triage](tryhackme/mirrorblast-c2-analysis/) | PCAP C2 triage (MirrorBlast / TA505) | [DOCX](tryhackme/mirrorblast-c2-analysis/report/mirrorblast-c2-triage.docx) |
| [Endpoint Intrusion Analysis](tryhackme/splunk-endpoint-forensics/) | Splunk/Sysmon endpoint intrusion | [DOCX](tryhackme/splunk-endpoint-forensics/report/endpoint-intrusion-analysis.docx) |

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
