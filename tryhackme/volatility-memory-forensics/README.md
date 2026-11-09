# Volatility Memory Forensics — Two Case Analysis

> TryHackMe · Memory forensics on two images with **Volatility 3** — a banking trojan and a WannaCry infection.

## Overview

A memory-forensics investigation of two acquired memory images: Investigation 1 (banking trojan delivered via a malicious Adobe document) and Investigation 2 (WannaCry ransomware). Work covered host profiling, process inspection, module/DLL analysis, IOC extraction, and malware-family attribution.

## Tools

Volatility 3 Framework; standard Linux utilities (`grep`, `strings`).

## Investigation 1 — Banking Trojan

- **Host:** Windows XP (build 2600), system time `2012-07-22 02:45:08`.
- **Suspicious process:** `reader_sl.exe` (PID 1640), parent `explorer.exe` (PID 1636) — impersonating Adobe Reader.
- **Network:** memory strings show access to online-banking domains (Chase) — consistent with credential harvesting.
- **User-agent:** `Mozilla/5.0 (Windows; U; MSIE 7.0; Windows NT 6.0; en-US)`.

## Investigation 2 — WannaCry Ransomware

- **Suspicious process:** `WanaDecryptor.exe` (PID 740) at `C:\Intel\ivecucqmanpnirkt615\WanaDecryptor@.exe`.
- **Parent:** `tasksche.exe` (PID 1940) — abused for persistence.
- **Attribution:** WannaCry (process name, directory structure, mutexes, DLL loads).
- **Networking DLL:** `ws2_32.dll` (Windows Sockets) loaded for C2.
- **Mutexes:** `ShimCacheMutex`, `MsWinZonesCacheCounterMutexA`, `MsWinZonesCacheCounterMutexA0`.

## Indicators of compromise

| Case | Type | Indicator |
|---|---|---|
| 1 | Process | `reader_sl.exe` (PID 1640) |
| 1 | User-agent | `MSIE 7.0; Windows NT 6.0` |
| 2 | Process | `WanaDecryptor.exe` (PID 740) |
| 2 | Path | `C:\Intel\ivecucqmanpnirkt615\WanaDecryptor@.exe` |
| 2 | Mutex | `MsWinZonesCacheCounterMutexA` |

## Evidence

![Case 1 — malfind suspicious process](evidence/screenshots/3_case1_malfind_suspicious_process.png)
![Case 1 — banking domain evidence](evidence/screenshots/6_case1_suspicious_bank_domain.png)
![Case 2 — WannaCry process](evidence/screenshots/7_case2_suspicious_process.png)
![Case 2 — WannaCry mutex indicator](evidence/screenshots/9_case2_mutex_indicator_of_malware.png)

All 9 screenshots are in [`evidence/screenshots/`](evidence/screenshots/).

## Full report

📄 [volatility_memory_forensics_report.pdf](report/volatility_memory_forensics_report.pdf)

---

*Skills: process/DLL inspection, parent-child reconstruction, network-indicator extraction, mutex analysis, malware attribution. Originally published at `github.com/hordiikorol/volatility-memory-forensics`.*
