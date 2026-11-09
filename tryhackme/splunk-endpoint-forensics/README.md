# Endpoint Intrusion Analysis (Splunk)

> TryHackMe · Splunk + Sysmon investigation of a compromised **Finance workstation** at Widget LLC, during a window when endpoint security was disabled. · Case `THM-SPL-NH01`

## Overview

A forensic investigation, via Splunk Enterprise, into a compromised Finance-department workstation. The intrusion was multi-stage and occurred while endpoint protection was disabled. Findings include credential-harvesting tools, PowerShell/WMIC defense evasion, anti-forensics, and multiple persistence points.

## Tools

Splunk (SPL) over Windows Event Logs + **Sysmon** (process creation ID 1, network ID 3, DLL load ID 7); VirusTotal.

## Key findings

- **Credential harvesting:** `C:\Users\FINANC~1\AppData\Local\Temp\11111.exe` — a renamed **`ChromeCookiesView.exe`** (NirSoft).
- **Malicious payload:** `IonicLarge.exe` (orig. `PalitExplorer.exe`), 54/70 on VirusTotal, C2 **`2.56.59.42`**.
- **Defense evasion:** PowerShell + WMIC disabled Windows Defender via `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender`, setting exclusion IDs `2147735503`, `2147737010`, `2147737007`, `2147737394`.
- **Anti-forensics:** killed processes and deleted `WvmIOrcfsuILdX6SNwIRmGOJ.exe`, `phcIAmLJMAIMSa9j9MpgJo1m.exe`.
- **Secondary persistence (DLL side-loading):** `C:\Users\Finance01\AppData\Roaming\EasyCalc\EasyCalc.exe` loading `ffmpeg.dll`, `nw.dll`, `nw_elf.dll`.

## Indicators of compromise

| Type | Indicator |
|---|---|
| Credential tool | `11111.exe` = `ChromeCookiesView.exe` (NirSoft) |
| Malware | `IonicLarge.exe` (`PalitExplorer.exe`) |
| C2 IP | `2.56.59.42` |
| Side-loader | `EasyCalc.exe` + `ffmpeg.dll`, `nw.dll`, `nw_elf.dll` |
| Deleted binaries | `WvmIOrcfsuILdX6SNwIRmGOJ.exe`, `phcIAmLJMAIMSa9j9MpgJo1m.exe` |

## Full report

📄 [endpoint-intrusion-analysis.docx](report/endpoint-intrusion-analysis.docx)

---

*Analyst: Hordii Korol. Skills: Splunk/Sysmon correlation, defense-evasion detection, DLL side-loading analysis, IOC extraction. Originally published at `github.com/hordiikorol/Splunk-Endpoint-Forensics`.*
