# RUN_POWERSHELL_SCRIPT_ON_REMOTE_COMPUTER
PowerShell Remote Management (WinRM) Configuration Documentation

1. Enable-PSRemoting

  The Enable-PSRemoting cmdlet configures the computer to receive remote PowerShell commands. It performs the following tasks:

  **Enable-PSRemoting**

2. Set Network Connection Profile to Private

  This command sets the network connection profile to Private, allowing private network communication.

  **Get-NetConnectionProfile | Set-NetConnectionProfile -NetworkCategory Private**

3. Enable PSRemoting with SkipNetworkProfileCheck and Force

  Enables PSRemoting with the -SkipNetworkProfileCheck parameter to skip the network profile check, and the -Force parameter to suppress confirmation prompts.

  **Enable-PSRemoting –SkipNetworkProfileCheck -Force**

4. Set NetFirewallRule for WINRM-HTTP-In-TCP

  Configures the firewall rule "WINRM-HTTP-In-TCP" to allow incoming TCP connections on any remote address.

  **Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP" -RemoteAddress Any**

5. Set NetFirewallRule for  WINRM-HTTP-In-TCP-NoScope

  Configures another firewall rule "WINRM-HTTP-In-TCP-NoScope" to allow incoming TCP connections on any remote address.

  **Set-NetFirewallRule -Name "WINRM-HTTP-In-TCP-NoScope" -RemoteAddress Any**

6. Open Firewall Ports for WinRM

  Creates firewall rules to allow inbound connections on specific TCP ports (5985 for HTTP and 5986 for HTTPS).

  **New-NetFirewallRule -Name WinRM-HTTP-In-TCP -DisplayName 'WinRM HTTP Inbound' -Enabled True -Direction Inbound -Protocol TCP -LocalPort 5985**

  **New-NetFirewallRule -Name WinRM-HTTPS-In-TCP -DisplayName 'WinRM HTTPS Inbound' -Enabled True -Direction Inbound -Protocol TCP -LocalPort 5986**

7. Check WinRM Configuration

  Displays the current WinRM configuration settings.

  **winrm get winrm/config**


8. Configure Trusted Hosts on Local Computer 

  Sets the trusted hosts on the local computer for WinRM communication.

  **winrm set winrm/config/client '@{TrustedHosts="54.167.92.97"}'**

9. Configure Credentials on Local Computer 

  Sets the credentials on the local computer to invoke the command directly.

**$credential = New-Object System.Management.Automation.PSCredential ("Administrator", (ConvertTo-SecureString -String "2JVbshDWj3r?HwZmgcN3NV3!3yz;9F5l" -    AsPlainText -Force))
**

10. Execute Script on Remote Computer

  Runs a PowerShell script on the remote computer using the Invoke-Command cmdlet and specifying the script block and credentials.

  **Invoke-Command -ScriptBlock {C:\Users\Administrator\Downloads\Script.ps1} -ComputerName 54.167.92.97 -Credential $credential**




























