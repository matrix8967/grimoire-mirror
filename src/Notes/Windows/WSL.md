# WSL

### Set Default WSL to Ver. 2:

```powershell
wsl --set-default-version 2
```

### Backup a WSL Distro
```powershell
wsl --export $DISTRO $PATH_TO_BACKUP.tar
```
### Restore a WSL Distro from Backup
```powershell
wsl --import $DISTRO $INSTALL_DIR $PATH_TO_BACKUP.tar
```