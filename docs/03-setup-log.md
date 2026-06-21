# Setup Log

## 1. UTM Installation
UTM was installed on macOS to create an isolated Windows-based virtual machine for cybersecurity research. The virtual machine approach was selected to keep the research environment separated from the host system.

### Why UTM was used
- Free and suitable for students
- Works well on MacBook systems
- Provides isolation between host and guest systems
- Appropriate for controlled cybersecurity lab work

## 2. Windows 11 Virtual Machine Creation
A Windows 11 ARM virtual machine was created in UTM.

### Configuration
- Memory: 4 GB RAM
- Storage: 60 GB
- Shared folder: Disabled
- Network: Default UTM shared network
- Guest tools: Enabled
- Device name: CyberLab-01

### Security decision
Shared folders were intentionally disabled to reduce direct interaction between the Windows VM and the host macOS environment.

## 3. Windows Installation
Windows 11 was installed successfully inside the virtual machine. During installation, the system initially attempted to boot repeatedly from the ISO image. This issue was resolved by removing the Windows installation ISO after the operating system files had been copied.

### Problem encountered
The VM entered an installation loop because it continued booting from the Windows setup media.

### Resolution
The Windows ISO was ejected from the virtual CD/DVD drive, allowing the VM to boot from the installed Windows system instead.

## 4. PowerShell Logging Setup
PowerShell was opened with Administrator privileges to enable advanced logging features required for this research project.

## 5. Execution Policy Command
Command used:
`Set-ExecutionPolicy Unrestricted -Force`

### Meaning
This command changes the PowerShell execution policy to allow scripts and commands to run without interactive confirmation prompts. This was used only inside the lab VM to simplify controlled testing.

## 6. Script Block Logging
Command used:
`New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force`

### Meaning
This command creates the registry path used by Windows to store the Script Block Logging configuration.

Command used:
`Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name "EnableScriptBlockLogging" -Value 1`

### Meaning
This command enables Script Block Logging, which records PowerShell code blocks executed in the system. This is important because it helps capture the content of PowerShell commands and scripts for later analysis.

## 7. Module Logging
Command used:
`New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Force`

### Meaning
This command creates the registry path for Module Logging configuration.

Command used:
`Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging" -Name "EnableModuleLogging" -Value 1`

### Meaning
This command enables Module Logging, which records activity related to PowerShell modules used during execution.

Command used:
`New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging\ModuleNames" -Force`

### Meaning
This creates the subkey used to define which modules should be logged.

Command used:
`Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging\ModuleNames" -Name "*" -Value "*"`

### Meaning
This configures Windows to log all PowerShell modules rather than a limited subset.

## 8. Restart
The Windows virtual machine was restarted after registry-based logging changes were made.

### Why restart was needed
A restart was necessary to ensure the logging policy changes were applied correctly.

## 9. Verification of Logging
After restart, PowerShell was opened and the following command was executed:

`Get-Date`

### Meaning
This command prints the current system date and time. It was used as a harmless test command to confirm that PowerShell logging was functioning.

### Verification method
Event Viewer was opened and the following log location was checked:

`Applications and Services Logs > Microsoft > Windows > PowerShell > Operational`

New events appeared after running the test command, confirming that logging was successfully enabled.

## 10. Current Stage
The environment is now ready for dataset generation. The next step is to execute both benign and suspicious PowerShell commands and collect the resulting operational logs for behavioral analysis.
