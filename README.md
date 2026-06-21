# Behavioral Detection of Suspicious PowerShell Activity Using Windows Event Logs

## Project Overview

This project investigates whether suspicious PowerShell activity can be identified through behavioural analysis of Windows PowerShell Operational Logs in a controlled virtual machine environment. The project focuses on **analysing PowerShell command execution behaviour rather than relying solely on signatures or known malicious files**. By comparing benign administrative activity with suspicious execution techniques, the project demonstrates how behavioural indicators can support threat detection and investigation.

## Research Question

**Can suspicious PowerShell execution be identified using behavioural indicators extracted from PowerShell Operational Logs?**


## Project Objectives

* Build a controlled Windows laboratory environment
* Verify PowerShell logging capabilities
* Generate benign PowerShell activity
* Generate suspicious PowerShell activity in a safe manner
* Analyse PowerShell Operational Log events
* Identify behavioural indicators associated with suspicious activity
* Map observed behaviours to the MITRE ATT&CK framework
* Evaluate the effectiveness of behavioural monitoring approaches

## Lab Environment

| Component              | Details                                  |
| ---------------------- | ---------------------------------------- |
| Host System            | macOS                                    |
| Hardware               | Apple Silicon MacBook Pro                |
| Hypervisor             | UTM                                      |
| Guest Operating System | Windows 11 Home ARM64                    |
| Shell                  | Windows PowerShell                       |
| Log Source             | Microsoft-Windows-PowerShell/Operational |
| Event IDs Analysed     | 4103, 4104                               |


## Methodology

The project followed a behavioural analysis approach consisting of four phases:

### 1. Logging Verification

PowerShell Operational Logging was verified within the Windows virtual machine environment.

The following event IDs were identified:

| Event ID | Description          |
| -------- | -------------------- |
| 4103     | Module Logging       |
| 4104     | Script Block Logging |

### 2. Benign Activity Generation

Common administrative PowerShell commands were executed and analysed:

```powershell
Get-Process
Get-Service
Get-ChildItem
Get-ComputerInfo
Get-Location
```

### 3. Suspicious Activity Simulation

Safe commands associated with attacker reconnaissance and suspicious execution behaviour were generated:

```powershell
Get-LocalUser
Get-NetIPAddress
Get-NetTCPConnection

powershell -NoProfile -Command "Get-Process"
powershell -WindowStyle Hidden -Command "Get-Service"
```

### 4. Behavioural Analysis

PowerShell Operational Logs were reviewed to identify:

* Account discovery behaviour
* Network discovery behaviour
* Process discovery behaviour
* Hidden PowerShell execution
* NoProfile execution behaviour

Observed activities were then mapped to **MITRE ATT&CK techniques.**



## Behavioural Indicators Identified

| Behavioural Indicator           | Description                                              |
| ------------------------------- | -------------------------------------------------------- |
| Account Discovery               | Enumeration of local user accounts                       |
| Network Configuration Discovery | Collection of IP address information                     |
| Network Connection Discovery    | Enumeration of active network connections                |
| Process Discovery               | Inspection of running processes                          |
| Hidden PowerShell Execution     | PowerShell executed without visible console window       |
| NoProfile Execution             | PowerShell executed without loading user profile scripts |


## MITRE ATT&CK Mapping

| Observed Activity              | MITRE ATT&CK Technique                         |
| ------------------------------ | ---------------------------------------------- |
| Get-Process                    | T1057 – Process Discovery                      |
| Get-ComputerInfo               | T1082 – System Information Discovery           |
| Get-LocalUser                  | T1087 – Account Discovery                      |
| Get-NetIPAddress               | T1016 – System Network Configuration Discovery |
| Get-NetTCPConnection           | T1049 – System Network Connections Discovery   |
| PowerShell Execution           | T1059.001 – PowerShell                         |
| PowerShell -NoProfile          | T1059.001 – PowerShell                         |
| PowerShell -WindowStyle Hidden | T1059.001 – PowerShell                         |


## Key Findings

The project demonstrated that PowerShell Operational Logs provide valuable visibility into command execution behaviour. Event ID 4104 successfully captured executed PowerShell commands and execution parameters, allowing both benign and suspicious activities to be analysed.

A key finding was that **command context is often more important than the command itself.** For example, a command such as:

```powershell
Get-Service
```

may represent normal administrative activity.

However:

```powershell
powershell -WindowStyle Hidden -Command "Get-Service"
```

introduces behavioural indicators commonly associated with stealth execution techniques. This highlights the value of behavioural monitoring over simple command based detection.



## Repository Structure

```text
powershell-behavior-detection-research/

README.md

docs/
├── setup-log.md
├── methodology.md
├── logging-verification.md
├── benign-activity-analysis.md
├── suspicious-activity-analysis.md
├── behavioural-indicators.md
├── mitre-attack-mapping.md
├── findings-and-limitations.md

screenshots/
```

## Screenshots Included

* PowerShell Operational Log verification
* Event ID 4103 and 4104 verification
* Script Block Logging verification
* Benign command execution examples
* Discovery activity examples
* Suspicious PowerShell execution examples


## Project Outcomes

This project successfully demonstrated how PowerShell Operational Logs can be used to identify behavioural indicators of suspicious activity. By combining PowerShell logging, behavioural analysis and MITRE ATT&CK mapping, the project showed how security analysts can move beyond signature-based detection and focus on attacker behaviours and operational context.

## Future Work

Potential future enhancements include:

* Sysmon integration
* Windows Security Event Log correlation
* Detection rule development
* Microsoft Sentinel integration
* Alert prioritisation research
* Behaviour-based threat hunting
* AI-assisted alert analysis
* PowerShell and Sysmon telemetry correlation
