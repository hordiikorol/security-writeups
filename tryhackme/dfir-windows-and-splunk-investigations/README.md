# Investigating with Splunk — Log Intrusion Analysis

> TryHackMe · DFIR over Windows security + PowerShell logs ingested into **Splunk** (12,256 events).

## Overview

A log-analysis investigation performed in Splunk against Windows telemetry from several hosts. The goal was to identify unauthorized account creation, registry persistence, malicious PowerShell, and attacker C2, correlating events across the dataset.

## Tools

Splunk Enterprise (SPL search + event correlation), Windows Security / PowerShell operational logs, CyberChef (Base64 decoding), VirusTotal.

## Key findings

- **Backdoor account:** attacker created user **`Alberto`**.
- **SAM persistence:** registry modification at `HKLM\SAM\SAM\Domains\Account\Users\Names\Alberto`.
- **Impersonation:** adversary attempted to impersonate legitimate user **`James`**.
- **Remote account creation (WMIC):** `WMIC.exe /node:WORKSTATION6 process call create "net user /add Alberto paw0rd1"`.
- **Compromised host:** all malicious events originate from **`James.browne`**.
- **Malicious PowerShell:** encoded execution — 97 pipeline-execution / 79 executing-pipeline events.
- **Payload:** Base64 PowerShell revealed AMSI bypass, custom HTTP user-agent spoofing, and download-and-execute.
- **C2:** decoded script beacons to **`http://10.10.10.5/news.php`**.

## Indicators of compromise

| Type | Indicator |
|---|---|
| Backdoor user | `Alberto` (password `paw0rd1`) |
| Impersonated user | `James` |
| Compromised host | `James.browne` |
| Remote exec | `WMIC /node:WORKSTATION6 … net user /add` |
| C2 URL | `http://10.10.10.5/news.php` |
| Persistence | SAM key for `Alberto` |

## Evidence

![Unauthorized account creation](evidence/screenshots/2_new_account.png)
![Remote WMIC account-creation command](evidence/screenshots/5_account_creation_command.png)
![Base64 PowerShell decoding](evidence/screenshots/9_base_64_decoding.png)
![Defanged C2 URL](evidence/screenshots/10_defanged_url.png)

All 10 screenshots are in [`evidence/screenshots/`](evidence/screenshots/).

## Full report

📄 [splunk_log_intrusion_analysis.pdf](report/splunk_log_intrusion_analysis.pdf)

---

*Skills: SPL querying, event correlation, registry-persistence analysis, encoded-payload decoding, C2 identification. Originally published at `github.com/hordiikorol/dfir-windows-and-splunk-investigations`.*
