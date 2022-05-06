# Windows

In newer versions of Win10 and Win11 - Microsoft has fully committed to one of their favorite `UI/UX` traps: forcing users into having no choice but to use their invasive adware masquerading as services. 🙄️

Thankfully - with a bit of unnecessary elbow grease - you can force the Windows `OOBE` (Out Of Box Experience) to _fuck off_ and allow you to setup a _local user_ account without anchoring it to Microsoft's online "services."

## Windows 10 / Windows 11 OOBE Local Account Setup:

-   Get to _Sign In With Microsoft Account_ in OOBE.
-   `Shift` + `F10` to launch terminal.
-   Type: `ncpa.cpl`
-   Disable Network Device Adapter(s).
-   Go back to OOBE, retry User Setup.
-   After setup is complete you can re-enable your Network Device Adapters.

## Windows Product Key retrieval:

`wmic path SoftwareLicensingService get OA3xOriginalProductKey`

## Debloat tools:

`https://www.oo-software.com/en/shutup10`

`https://github.com/builtbybel/privatezilla`

## Windows Native SSH:

[Github Releases.](https://github.com/PowerShell/Win32-OpenSSH/releases)

[Docs.](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_server_configuration)

[Github Wiki.](https://github.com/powershell/win32-openssh/wiki)

## Windows Terminal:

[Source.](https://github.com/Microsoft/Terminal)

[Github Releases.](https://github.com/microsoft/terminal/releases)

[MS Store Link.](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=en-us&gl=US)

[Docs.](https://docs.microsoft.com/en-us/windows/terminal/)

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

## Ubuntu & Active Directory:

```
https://ubuntu.com//blog/ubuntu-21-04-is-here
https://github.com/ubuntu/adsys
https://github.com/ubuntu/adsys/tree/main/internal/policies/ad/definitions/policy/Ubuntu/all
https://ubuntu.com/server/docs/service-sssd
https://warlord0blog.wordpress.com/2020/02/04/tunnelling-rdp-over-ssh/
```
