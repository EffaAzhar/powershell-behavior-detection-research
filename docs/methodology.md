# Methodology

## Lab Design
The project uses a Windows 11 virtual machine running inside UTM on a MacBook Pro. The virtual machine acts as a controlled research environment for producing PowerShell activity and collecting logs.

## Data Collection Strategy
Two categories of PowerShell activity will be generated:

1. Benign activity
   - Regular administrative and system information commands
2. Suspicious activity
   - Commands that use behaviors often associated with attacker tradecraft, such as bypass flags, hidden window execution, or no-profile execution

## Logging Source
The primary source of data is the PowerShell Operational log in Event Viewer.

## Research Goal
The collected commands and logs will be analyzed using Python to identify behavioral indicators such as:
- command length
- entropy
- suspicious flags
- execution context

## Expected Outcome
The project aims to determine whether suspicious PowerShell behavior can be separated from benign activity through log-based behavioral analysis.
