# Incident Analysis Report: MirrorBlast C2 Triage

> TryHackMe · PCAP triage of a Malware Command-and-Control alert.
> **Analyst:** Hordii Korol · **Date:** January 27, 2026 · **Case ID:** `THM-WZ1-2026`

## 1. Executive summary

This report documents the forensic investigation of a high-priority network alert involving "Malware Command and Control Activity." Through systematic PCAP analysis, the activity was confirmed as a **True Positive**. The infection is attributed to the **MirrorBlast** malware family, a tool frequently utilized by the threat-actor group **TA505** (also known as Hive0065 or Graceful Spider).

## 2. Methodology & toolset

The investigation used a standard SOC L1 toolkit to identify, verify, and trace the attack lifecycle:

- **Brim** — log aggregation and initial signature identification.
- **Wireshark** — deep packet inspection (DPI) and protocol analysis.
- **VirusTotal** — threat intelligence and actor attribution.
- **CyberChef** — sanitization and defanging of malicious IoCs.

## 3. Investigation details

### 3.1 Alert identification

Initial triage in Brim identified critical IDS signatures originating from an internal host.

- **Alert signature:** `ET MALWARE MirrorBlast CnC Activity M3`
- **Source IP:** `172.16.1.102`
- **Destination IP:** `169.239.128.11`

### 3.2 Threat-intelligence attribution

The destination IP was correlated against global threat feeds to confirm its malicious status and intent.

- **Threat actor:** TA505
- **Malware family:** MirrorBlast
- **Primary vector:** Windows Installer (`.msi`) delivery via HTTP.

### 3.3 Protocol analysis

Deep packet inspection revealed the specific communication methods used by the stager to reach the C2 server.

- **User-Agent:** `REBOL View 2.7.8.3.1`
- **Request method:** HTTP GET with encoded parameters.

## 4. Attack retrace & infrastructure

The attack lifecycle involved distributed infrastructure to provide redundancy for payload delivery.

### 4.1 Associated infrastructure

Investigation of the source IP's HTTP history identified additional malicious endpoints.

- **Secondary IP 1:** `185.10.68.235`
- **Secondary IP 2:** `192.36.27.92`

### 4.2 Malicious artifacts

The following artifacts, representing the initial infection stagers, were retrieved from the network traffic:

- `filter.msi`
- `10opd3r_load.msi`

## 5. Host-based impact & persistence

The stagers were configured to drop malicious binaries into non-standard system directories to evade detection.

### 5.1 Persistence group A

- **Directory:** `C:\ProgramData\001\`
- **Artifacts:** `arab.bin`, `arab.exe`

### 5.2 Persistence group B

- **Directory:** `C:\ProgramData\Local\Google\`
- **Artifacts:** `rebol-view-278-3-1.exe`, `exemple.rb`

## 6. Conclusion

The investigation confirms a successful compromise of host `172.16.1.102`. The presence of specialized Rebol interpreters and hidden script files in the `\ProgramData\` directory indicates a sophisticated attempt at maintaining long-term access.

## Indicators of compromise

| Type | Indicator |
|---|---|
| Infected host | `172.16.1.102` |
| C2 IP | `169.239.128.11` |
| Secondary IPs | `185.10.68.235`, `192.36.27.92` |
| User-Agent | `REBOL View 2.7.8.3.1` |
| Stagers | `filter.msi`, `10opd3r_load.msi` |
| Dropped files | `arab.exe`, `arab.bin`, `rebol-view-278-3-1.exe`, `exemple.rb` |

---

*Full original report (DOCX): [mirrorblast-c2-triage.docx](report/mirrorblast-c2-triage.docx). Originally published at `github.com/hordiikorol/MirrorBlast-C2-Analysis`.*
