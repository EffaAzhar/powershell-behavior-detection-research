# Data Generation

## Objective
To generate a controlled dataset of PowerShell activity consisting of both benign and suspicious command executions for behavioral analysis.

---

## 1. Benign Commands

The following commands represent normal administrative or user activity:

### Commands used
- Get-Process
- Get-Service
- Get-Date
- Get-ChildItem C:\
- Test-Connection google.com

### Description

- **Get-Process**  
  Retrieves a list of running processes on the system.  
  Represents normal system monitoring activity.

- **Get-Service**  
  Displays system services and their status.  
  Common administrative command.

- **Get-Date**  
  Returns the current system date and time.  
  Used as a simple test command.

- **Get-ChildItem C:\\**  
  Lists files and directories in the C drive.  
  Represents normal file system interaction.

- **Test-Connection google.com**  
  Sends network ping requests to test connectivity.  
  Represents normal network usage.

---

## 2. Suspicious Commands (Simulated)

The following commands simulate behaviors commonly associated with malicious PowerShell usage.

### Commands used
- powershell -ExecutionPolicy Bypass
- powershell -NoProfile -Command "Get-Process"
- powershell -WindowStyle Hidden -Command "Get-Service"

### Description

- **ExecutionPolicy Bypass**  
  Disables PowerShell script execution restrictions.  
  Often used by attackers to run unauthorized scripts.

- **NoProfile**  
  Runs PowerShell without loading user profile scripts.  
  Used to avoid detection or logging tied to profiles.

- **WindowStyle Hidden**  
  Executes PowerShell commands without visible window.  
  Common technique for stealth execution.

---

## 3. Data Collection Method

After executing the commands, logs were collected from:

Applications and Services Logs  
→ Microsoft  
→ Windows  
→ PowerShell  
→ Operational

---

## 4. Logging Details

Key Event IDs observed:

- **4104** — Script Block Logging  
  Captures executed PowerShell code blocks

- **4103** — Module Logging  
  Captures module usage details

---

## 5. Dataset Purpose

The dataset will be used to:

- Compare benign vs suspicious behavior
- Identify distinguishing patterns
- Develop detection logic based on:
  - command structure
  - execution flags
  - behavioral indicators

---

## 6. Current Status

Data generation has started and logs are successfully being recorded.  
Next step is exporting logs and performing analysis using Python.
