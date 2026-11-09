Volatility Memory Forensics – DFIR Case Analysis

This repository contains a complete Digital Forensics and Incident Response (DFIR) investigation performed on two memory images using Volatility 3. The analysis includes host profiling, process inspection, malware attribution, detection of suspicious indicators, and confirmation of ransomware activity. The goal of this project is to demonstrate practical memory forensics skills typically required for SOC, IR, and DFIR analyst roles.

Contents

Volatility_Memory_Forensics_Report.pdf
Full written report documenting findings from Investigation 1 (Banking Trojan) and Investigation 2 (WannaCry ransomware).

evidence/screenshots/
Directory containing all screenshots referenced in the report.

Tools Used

Volatility 3 Framework
Used to analyze Windows memory artifacts, enumerate processes, inspect DLLs, extract strings, and identify indicators of compromise.

Standard Linux utilities (grep, strings, etc.)

Case Summaries
Investigation 1 – Banking Trojan

A memory dump from a quarantined endpoint was analyzed. Key findings include:

Malicious process impersonating Adobe Reader (reader_sl.exe)

Evidence of online banking domain access

Suspicious user-agent consistent with credential-harvesting malware

Process tree anomalies and injected code regions

Investigation 2 – WannaCry Ransomware

A second memory dump revealed:

Active WannaCry decryptor process (WanaDecryptor.exe)

Malicious file path and persistence mechanism

Known WannaCry mutex artifacts

DLLs used for network communication

Skills Demonstrated

Memory acquisition interpretation

Malware process identification

Parent/child process reconstruction

Network indicator extraction

Mutex and DLL analysis

Malware family attribution

Professional DFIR report creation

Directory Structure
volatility-memory-forensics/
│
├── Volatility_Memory_Forensics_Report.pdf
├── README.md
└── evidence/
    └── screenshots/