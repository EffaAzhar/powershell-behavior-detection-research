# MITRE ATT&CK Mapping

## Objective

The objective of this phase was to map observed PowerShell behaviours to the MITRE ATT&CK framework in order to better understand the security significance of each activity.
MITRE ATT&CK provides a structured knowledge base of adversary tactics and techniques. Mapping PowerShell activity to ATT&CK techniques helps translate raw log data into meaningful behavioural indicators. MITRE ATT&CK mapping was performed manually by analysing the purpose of each PowerShell command and identifying the corresponding adversary technique documented within the MITRE ATT&CK framework. This process transformed raw command execution logs into recognised attacker behaviours, supporting behavioural monitoring and threat analysis.


## Behaviour Mapping

| Observed Activity | Event ID | Behaviour | MITRE ATT&CK Technique |
|------------------|----------|-----------|------------------------|
| Get-Process | 4104 | Process Discovery | T1057 |
| Get-ComputerInfo | 4104 | System Information Discovery | T1082 |
| Get-LocalUser | 4104 | Account Discovery | T1087 |
| Get-NetIPAddress | 4104 | Network Configuration Discovery | T1016 |
| Get-NetTCPConnection | 4104 | Network Connections Discovery | T1049 |
| PowerShell Execution | 4104 | Command and Scripting Interpreter | T1059.001 |
| PowerShell -NoProfile | 4104 | PowerShell Execution | T1059.001 |
| PowerShell -WindowStyle Hidden | 4104 | Stealthy PowerShell Execution | T1059.001 |



## Benefits of MITRE ATT&CK Mapping

MITRE ATT&CK mapping transforms individual PowerShell commands into recognised adversary behaviours.

This approach supports:

- Behavioural monitoring
- Threat hunting
- Security investigations
- Detection engineering
- Alert prioritisation

Rather than focusing on individual commands, analysts can focus on attacker objectives and behavioural patterns.


## Findings

The PowerShell activities observed during this project successfully mapped to several MITRE ATT&CK techniques related to discovery and command execution. The mapping process demonstrated how PowerShell Operational Logs can support behavioural monitoring by providing visibility into activities commonly associated with attacker reconnaissance and PowerShell based operations.
