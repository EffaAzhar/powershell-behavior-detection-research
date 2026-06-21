# Findings and Limitations

## Research Question

Can suspicious PowerShell activity be identified using behavioural indicators extracted from PowerShell Operational Logs?


## Key Findings

The project demonstrated that PowerShell Operational Logs provide valuable visibility into command execution behaviour.

Event ID 4104 successfully recorded executed PowerShell commands and execution parameters, allowing both benign and suspicious activities to be analysed.

The following behaviours were successfully identified:

- Process discovery
- Account discovery
- Network configuration discovery
- Network connection discovery
- PowerShell execution using NoProfile
- PowerShell execution using Hidden Window Style

These behaviours were mapped to MITRE ATT&CK techniques and analysed from a behavioural monitoring perspective.


## Importance of Context

One of the most important findings was that command names alone are often insufficient for determining whether activity is suspicious.

For example:

```powershell
Get-Process
```

may represent normal administrative activity.

However:

```powershell
powershell -NoProfile -Command "Get-Process"
```

introduces additional behavioural context that may warrant further investigation.

This demonstrates the importance of behavioural analysis rather than relying solely on individual command names.


## Benefits of Behavioural Monitoring

Behavioural monitoring provides several advantages:

- Detects attacker behaviours rather than specific malware
- Supports threat hunting activities
- Aligns with MITRE ATT&CK methodology
- Provides context for security investigations
- Can identify suspicious activity even when commands vary


## Project Limitations

This project was conducted in a controlled virtual machine environment and therefore has several limitations:

- No real attack activity was executed
- Only a small number of PowerShell commands were analysed
- Analysis focused on PowerShell Operational Logs only
- Sysmon integration was not included in behavioural correlation
- Detection rules were not developed or tested


## Future Work

Future improvements may include:

- Sysmon integration
- Windows Security Event Log analysis
- Detection rule development
- SIEM integration using Microsoft Sentinel
- Alert prioritisation techniques
- AI-assisted behavioural analysis
- Larger datasets and attack simulations


## Conclusion

The project demonstrated that PowerShell Operational Logs can provide useful visibility into command execution behaviour.

Behavioural indicators such as account discovery, network discovery, hidden PowerShell execution, and NoProfile execution were successfully identified and mapped to MITRE ATT&CK techniques.

The findings support the use of behavioural monitoring as an effective approach for identifying potentially suspicious PowerShell activity within Windows environments.
