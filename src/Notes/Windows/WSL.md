# WSL

## Install WSL via CLI:

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## Enable Virtualization Support for WSL2:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## Set Default WSL to Ver. 2:

```powershell
wsl --set-default-version 2
```

## List Installed Distros:

```powershell
wsl -l [-v]
```

## Set Default Distro:

```powershell
wsl --set-default $DISTRO
```

## Force Distro to run WSL1:

```powershell
wsl --set-version $DISTRO 1
```

## Uninstall Distro:

```powershell
wsl --unregister $DISTRO
```

## Backup a WSL Distro
```powershell
wsl --export $DISTRO $PATH_TO_BACKUP.tar
```

## Restore a WSL Distro from Backup
```powershell
wsl --import $DISTRO $INSTALL_DIR $PATH_TO_BACKUP.tar
```
