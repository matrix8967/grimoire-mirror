# Windows

## Windows 10 / Windows 11 OOBE Local Account Setup:

In newer versions of Win10 and Win11 - Microsoft has fully committed to one of their favorite `UI/UX` traps: forcing users into having no choice but to use their invasive adware masquerading as services. 🙄️

Thankfully - with a bit of unnecessary elbow grease - you can force the Windows `OOBE` (Out Of Box Experience) to _fuck off_ and allow you to setup a _local user_ account without anchoring it to Microsoft's online "services."

-   Get to _Sign In With Microsoft Account_ in OOBE.
-   `Shift` + `F10` to launch terminal.
-   Type: `ncpa.cpl`
-   Disable Network Device Adapter(s).
-   Go back to OOBE, retry User Setup.
-   After setup is complete you can re-enable your Network Device Adapters.

-----

## Change RDP Port & Firewall Rules:

```
Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "PortNumber" -Value $PORT_NUMBER
New-NetFirewallRule -DisplayName 'RDPPORTLatest-TCP-In' -Profile 'Public' -Direction Inbound -Action Allow -Protocol TCP -LocalPort $PORT_NUMBER
New-NetFirewallRule -DisplayName 'RDPPORTLatest-UDP-In' -Profile 'Public' -Direction Inbound -Action Allow -Protocol UDP -LocalPort $PORT_NUMBER
```

## Windows Product Key retrieval:

`wmic path SoftwareLicensingService get OA3xOriginalProductKey`

## Windows Native SSH:

[Github Releases.](https://github.com/PowerShell/Win32-OpenSSH/releases)

[Docs.](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_server_configuration)

[Github Wiki.](https://github.com/powershell/win32-openssh/wiki)

## Windows Terminal:

[Source.](https://github.com/Microsoft/Terminal)

[Github Releases.](https://github.com/microsoft/terminal/releases)

[MS Store Link.](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=en-us&gl=US)

[Docs.](https://docs.microsoft.com/en-us/windows/terminal/)

## Debloat tools:

[O&O Shutup10](https://www.oo-software.com/en/shutup10)

[Privatezilla](https://github.com/builtbybel/privatezilla)

-----

## Scoop:

<https://scoop.sh/>

```
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
Invoke-Expression (New-Object System.Net.WebClient).DownloadString('https://get.scoop.sh')
```
### Disable Windows Defender Scanning for Scoop Dir:

```
Add-MpPreference -ExclusionPath "$($env:programdata)\scoop", "$($env:scoop)"
Add-MpPreference -ExclusionPath "$($env:programdata)\scoop"
```
### Re-enable Win Defender:
`Remove-MpPreference -ExclusionPath "$($env:programdata)\scoop", "$($env:scoop)"`

### Scoop Buckets:

```
scoop bucket add main
scoop bucket add extras
scoop bucket add versions
scoop bucket add nirsoft
scoop bucket add php
scoop bucket add nerd-fonts
scoop bucket add nonportable
scoop bucket add java
scoop bucket add games
```

-----

## Ubuntu & Active Directory:

```
https://ubuntu.com//blog/ubuntu-21-04-is-here
https://github.com/ubuntu/adsys
https://github.com/ubuntu/adsys/tree/main/internal/policies/ad/definitions/policy/Ubuntu/all
https://ubuntu.com/server/docs/service-sssd
```

-----

## Windows Package Manager:

`https://github.com/microsoft/winget-cli`
`https://github.com/microsoft/winget-pkgs`
`https://docs.microsoft.com/en-us/learn/modules/explore-windows-package-manager-tool/?WT.mc_id=AZ-MVP-5004737`
