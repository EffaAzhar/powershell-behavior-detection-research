# Behavioural Indicators

Identifying behavioural indicators that may help distinguish suspicious PowerShell activity from normal administrative usage. Behavioural indicators focus on how PowerShell is used rather than relying solely on specific command names. This approach aligns with modern cybersecurity monitoring practices where attacker behaviour is analysed in context.


## What is a Behavioural Indicator?

A behavioural indicator is an observable action, pattern, or characteristic that may suggest malicious or suspicious activity.

Unlike traditional signature based detection, behavioural analysis focuses on the context of the commands through following questions:

- How a command is executed
- What information is being gathered
- Whether stealth techniques are being used
- Whether multiple suspicious activities occur together


## Identified Behavioural Indicators

### 1. PowerShell Execution

Indicator:

```powershell
powershell.exe
```

Description:

The execution of PowerShell itself may be significant depending on the environment.

PowerShell is a legitimate administrative tool but is also widely abused by attackers due to its powerful scripting capabilities.

Security Relevance:

- Common attack vector
- Frequently used during post-exploitation activities

Observed Event ID:

- 4104


### 2. Account Discovery

Indicator:

```powershell
Get-LocalUser
```

Description:

Retrieves information about local user accounts.

Potential Security Significance:

Attackers commonly enumerate user accounts after obtaining access to a system in order to identify privileged users and potential targets for lateral movement.

Observed Event ID:

- 4104

MITRE ATT&CK:

- T1087 – Account Discovery


### 3. Network Configuration Discovery

Indicator:

```powershell
Get-NetIPAddress
```

Description:

Displays network interface and IP address information.

Potential Security Significance:

Attackers may gather network configuration details to better understand the environment and identify additional targets.

Observed Event ID:

- 4104

MITRE ATT&CK:

- T1016 – System Network Configuration Discovery


### 4. Network Connection Discovery

Indicator:

```powershell
Get-NetTCPConnection
```

Description:

Displays active TCP connections.

Potential Security Significance:

This command may reveal active communication channels, remote systems, and services currently in use.

Observed Event ID:

- 4104

MITRE ATT&CK:

- T1049 – System Network Connections Discovery


### 5. PowerShell NoProfile Execution

Indicator:

```powershell
powershell -NoProfile
```

Description:

Launches PowerShell without loading user profile scripts.

Potential Security Significance:

This behaviour is frequently observed during attacker activity because it creates a cleaner execution environment and reduces dependency on user-specific configurations.

Observed Event ID:

- 4104

MITRE ATT&CK:

- T1059.001 – PowerShell


### 6. Hidden PowerShell Execution

Indicator:

```powershell
powershell -WindowStyle Hidden
```

Description:

Executes PowerShell without displaying a visible console window.

Potential Security Significance:

Hidden execution is commonly associated with malware, persistence mechanisms and stealth techniques.

Observed Event ID:

- 4104

MITRE ATT&CK:

- T1059.001 – PowerShell

## Behavioural Indicator Summary

| Behavioural Indicator | Risk Level | Security Significance |
|----------------------|------------|-----------------------|
| Standard PowerShell Execution | Low | Common administrative activity |
| Get-LocalUser | Medium | Account discovery |
| Get-NetIPAddress | Medium | Network discovery |
| Get-NetTCPConnection | Medium | Connection discovery |
| PowerShell -NoProfile | High | Potential defence evasion |
| PowerShell -WindowStyle Hidden | High | Potential stealth execution |


## Why Context Matters

A key finding of this project is that PowerShell commands cannot always be classified as malicious or benign based solely on their names.

For example:

```powershell
Get-Service
```

is a normal administrative command.

However:

```powershell
powershell -WindowStyle Hidden -Command "Get-Service"
```

introduces a behavioural indicator associated with stealth execution. The command remains the same, but the execution context changes its security significance. This demonstrates **why behavioural monitoring focuses on how commands are executed rather than relying only on the command itself.**


## Findings

Several behavioural indicators were successfully identified through PowerShell Operational Log analysis. The analysis showed that Event ID 4104 provides valuable visibility into command execution behaviour and execution context. Discovery commands such as account enumeration and network reconnaissance may be legitimate when used by administrators but may also indicate attacker reconnaissance activities when observed in suspicious contexts. Similarly, execution parameters such as NoProfile and WindowStyle Hidden provide additional behavioural indicators that can support threat detection and investigation activities.
