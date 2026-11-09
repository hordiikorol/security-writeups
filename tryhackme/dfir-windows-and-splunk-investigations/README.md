Splunk Log Intrusion Analysis

This repository contains a complete Digital Forensics and Incident Response (DFIR) investigation performed using Splunk. All analysis was conducted on Windows security logs ingested into the Splunk platform. The goal of the investigation was to identify attacker activity, correlate events, and document indicators of compromise.

Contents

Splunk Intrusion Analysis Report
A full investigation detailing unauthorized account creation, SAM registry manipulation, user impersonation, remote WMIC execution, malicious PowerShell activity, and command-and-control communication.
The complete report is located at:
reports/investigating_with_splunk_intrusion_analysis.pdf

Evidence Screenshots
Screenshots that support the findings documented in the report.
Screenshots are located in:
evidence/screenshots/

Skills Demonstrated

• Log analysis using Splunk
• SPL querying and event correlation
• Identification of unauthorized account activity
• Registry persistence analysis
• Detection of remote code execution
• Analysis of encoded PowerShell payloads
• Identification of command-and-control traffic
• Professional DFIR-style documentation

Folder Structure

reports/
 investigating_with_splunk_intrusion_analysis.pdf

evidence/
 screenshots/

Purpose

This project demonstrates practical capabilities required for SOC Analyst, DFIR Analyst, and Threat Hunter roles. The investigation highlights the ability to identify attacker behavior through log correlation and structured forensic analysis.

How to Use

Open the PDF in the reports directory to view the full findings and analysis. Review the evidence screenshots to validate each step of the investigation.