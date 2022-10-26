# Post-Install

-----

### O&O Shutup 10:

[O&O Shutup 10](https://www.oo-software.com/en/shutup10) is an application that unobfuscates the various settings in Windows. It allows controlling settings, backup & restoration of settings, as well as recommendations and descriptions of advanced settings.

Each user should configure this based on their own usecase.

My `ooshutup10.cfg` file [here](../../Configs/Windows/ooshutup10.md).

-----

### Scoop:

[Scoop](https://scoop.sh/) is a 3rd party, community maintained Software Repository that makes automating & scripting the installation of Windows Packages easier.

Similar tools are _Chocolatey_, _Ninite_ as well as Microsoft's own official Package Manager that is still in testing called [Winget](https://github.com/microsoft/winget-pkgs).

#### Install Scoop:

```powershell
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

#### (Optional) Disable Windows Defender Scanning for Scoop Dir:

Hopefully, your default security configuration will prevent from running unsigned 3rd party scripts by default. However - this is required for the installationof `Scoop.`

To temporarily disable your default security policy for `Scoop` - run the following Powershell Commands:

```powershell
Add-MpPreference -ExclusionPath "$($env:programdata)\scoop", "$($env:scoop)"
Add-MpPreference -ExclusionPath "$($env:programdata)\scoop"
```

To Renable your default security policy (recommended) run the following:

```powershell
Remove-MpPreference -ExclusionPath "$($env:programdata)\scoop", "$($env:scoop)"
```

#### Scoop Buckets:

`Scoop` repos are called _Buckets._ You can add additional Repos (Buckets) via the following:

```
scoop bucket add main
scoop bucket add extras
scoop bucket add nerd-fonts
scoop bucket add nonportable
scoop bucket add games
```

Ensure you've inspected & trust the software repos before adding them.

Once you've configured `Scoop` and installed any applications -- you can backup your configuration & apps to a `json` file for future scripting/automation:

```powershell
scoop export -c > Scoopfile.json
```

You can import your backup config/apps using:

```powershell
scoop import Scoopfile.json
```

My `Scoopfile.json` can be found [here.](../../Configs/Windows/Scoopfile.md)

-----

## Windows Terminal:

[Source.](https://github.com/Microsoft/Terminal)

[Github Releases.](https://github.com/microsoft/terminal/releases)

[MS Store Link.](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=en-us&gl=US)

[Docs.](https://docs.microsoft.com/en-us/windows/terminal/)

[My Windows Terminal Config File.](../../Configs/Windows/WindowsTerminal.md)

-----

## Remote Mgmt:

### Windows Native SSH:

`SSH` is an incredibly versitle & powerful utility that allows secure, reliable remote connection via `CLI`.

Microsoft now has an official, native `SSH` implimentation without needing to rely on 3rd parties like `PuTTy`.

[Github Releases.](https://github.com/PowerShell/Win32-OpenSSH/releases)

[Docs.](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_server_configuration)

[Github Wiki.](https://github.com/powershell/win32-openssh/wiki)

```powershell

### Set Powershell as the default SSH Environment:

New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

For more `SSH` Configuration Options check my [SSH Notes.](../../Notes/SSH/SSH_Notes.md)

-----

### RDP:

Microsoft's `RDP` (Remote Desktop Protocol) has long been the defacto remote mgmt tool for Windows Environments.

It's _never_ a good idea to use the default `RDP` configuration & Port (`3389`).

Below is an example workflow for changing the default `RDP` port & updating your `Firewall` Configuration.

```powershell
Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "$NEW_RDP_PORT_NUMBER"
Get-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "3389"

Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber" -Value $NEW_RDP_PORT_NUMBER
New-NetFirewallRule -DisplayName 'RDPPORTLatest-TCP-In' -Profile 'Public' -Direction Inbound -Action Allow -Protocol TCP -LocalPort $NEW_RDP_PORT_NUMBER
New-NetFirewallRule -DisplayName 'RDPPORTLatest-UDP-In' -Profile 'Public' -Direction Inbound -Action Allow -Protocol UDP -LocalPort $NEW_RDP_PORT_NUMBER
```

-----

## Powershell:

`https://github.com/PowerShell/PowerShell`

Full Powershell History File:

`%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt`
