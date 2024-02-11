# PowerShell Remote Management (WinRM) Configuration Documentation

## Overview
PowerShell Remoting (WinRM) allows you to execute PowerShell commands on remote computers. This documentation outlines the steps to configure WinRM for efficient and secure remote management.

### 1. Enable-PSRemoting
The `Enable-PSRemoting` cmdlet configures the computer to receive remote PowerShell commands. It performs the following tasks:
- Enables PSRemoting on the local machine.

```powershell
Enable-PSRemoting
```

### 2. Set Network Connection Profile to Private
This command sets the network connection profile to Private, allowing private network communication.

```powershell
Get-NetConnectionProfile | Set-NetConnectionProfile -NetworkCategory Private
```

### 3. Enable PSRemoting with SkipNetworkProfileCheck and Force
Enables PSRemoting with the -SkipNetworkProfileCheck parameter to skip the network profile check, and the -Force parameter to suppress confirmation prompts.

```powershell
Enable-PSRemoting –SkipNetworkProfileCheck -Force
```

### 4. Configure Firewall Rules
Configure the following firewall rules to allow incoming TCP connections on any remote address:

a. WINRM-HTTP-In-TCP

```powershell
Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP" -RemoteAddress Any
```

b. WINRM-HTTP-In-TCP-NoScope

```powershell
Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-NoScope" -RemoteAddress Any
```

### 5. Open Firewall Ports for WinRM
Create firewall rules to allow inbound connections on specific TCP ports:

Port 5985 for HTTP
Port 5986 for HTTPS

```powershell
New-NetFirewallRule -Name WinRM-HTTP-In-TCP -DisplayName 'WinRM HTTP Inbound' -Enabled True -Direction Inbound -Protocol TCP -LocalPort 5985
New-NetFirewallRule -Name WinRM-HTTPS-In-TCP -DisplayName 'WinRM HTTPS Inbound' -Enabled True -Direction Inbound -Protocol TCP -LocalPort 5986
```

### 6. Check WinRM Configuration
Display the current WinRM configuration settings.

```powershell
winrm get winrm/config
```

### 7. Configure Trusted Hosts on Local Computer
Set the trusted hosts on the local computer for WinRM communication.

```powershell
winrm set winrm/config/client '@{TrustedHosts="54.167.92.97"}'
```


### Feel free to use and modify this content as needed for your `readme.md` file. If you have any other requests or need additional assistance, feel free to ask! 😊




