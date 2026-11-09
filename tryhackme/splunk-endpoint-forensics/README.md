# Incident Analysis Report: Endpoint Intrusion Analysis

> TryHackMe · Splunk + Sysmon investigation of a compromised Finance workstation.
> **Analyst:** Hordii Korol · **Date:** January 27, 2026 · **Case ID:** `THM-SPL-NH01`

## 1. Executive summary

This report details a forensic investigation into a compromised workstation within the Finance Department of Widget LLC. The investigation, conducted via Splunk Enterprise, identifies a multi-stage intrusion that occurred during a period when endpoint security products were disabled. Key findings include the execution of credential-harvesting tools, defense evasion via PowerShell, and the identification of persistent malicious binaries.

## 2. Methodology & toolset

The investigation used enterprise-grade telemetry and search capabilities:

- **Splunk (SPL)** — primary tool for searching and correlating Windows Event Logs and Sysmon data.
- **Sysmon** — tracked process creation (ID 1), network connections (ID 3), and DLL loads (ID 7).
- **VirusTotal** — external threat intelligence and malware-family attribution.

## 3. Investigation findings

### 3.1 Credential harvesting & execution

A malicious binary designed for credential theft was identified running from a temporary directory. This binary is a known password-viewing tool often repurposed by threat actors.

- **Malicious binary path:** `C:\Users\FINANC~1\AppData\Local\Temp\11111.exe`
- **Original filename:** `ChromeCookiesView.exe`
- **Company name:** NirSoft

### 3.2 Malicious payload analysis

A secondary suspicious binary was identified in the same directory, which triggered multiple high-severity alerts on VirusTotal (**54/70** detections).

- **Binary name:** `IonicLarge.exe`
- **Original filename:** `PalitExplorer.exe`
- **C2 IP address:** `2.56.59.42`

### 3.3 Defense evasion (Windows Defender)

The adversary used PowerShell and WMIC to systematically disable Windows Defender and set specific exclusion IDs to maintain access without detection.

- **Registry key target:** `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender`
- **Exclusion IDs set:** `2147735503`, `2147737010`, `2147737007`, `2147737394`

## 4. Host-based impact

### 4.1 Anti-forensics (process & file deletion)

Evidence was found of the attacker attempting to cover their tracks by killing active processes and deleting the associated binaries:

- `WvmIOrcfsuILdX6SNwIRmGOJ.exe`
- `phcIAmLJMAIMSa9j9MpgJo1m.exe`

### 4.2 Secondary malware execution

A separate malicious binary was identified in the Roaming profile, using DLL side-loading to execute malicious code.

- **Path:** `C:\Users\Finance01\AppData\Roaming\EasyCalc\EasyCalc.exe`
- **Loaded DLLs:** `ffmpeg.dll`, `nw.dll`, `nw_elf.dll`

## 5. Conclusion

The workstation was successfully compromised by an actor using credential harvesters and defense-evasion scripts. The presence of `IonicLarge.exe` and `EasyCalc.exe` indicates that the attacker established multiple points of persistence on the host.

## Indicators of compromise

| Type | Indicator |
|---|---|
| Credential tool | `11111.exe` = `ChromeCookiesView.exe` (NirSoft) |
| Malware | `IonicLarge.exe` (`PalitExplorer.exe`) |
| C2 IP | `2.56.59.42` |
| Side-loader | `EasyCalc.exe` + `ffmpeg.dll`, `nw.dll`, `nw_elf.dll` |
| Deleted binaries | `WvmIOrcfsuILdX6SNwIRmGOJ.exe`, `phcIAmLJMAIMSa9j9MpgJo1m.exe` |
| Defender exclusions | `2147735503`, `2147737010`, `2147737007`, `2147737394` |

---

*Full original report (DOCX): [endpoint-intrusion-analysis.docx](report/endpoint-intrusion-analysis.docx). Originally published at `github.com/hordiikorol/Splunk-Endpoint-Forensics`.*
