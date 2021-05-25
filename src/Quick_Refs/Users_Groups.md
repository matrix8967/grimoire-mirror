# Users & Groups copypasta.

`Idk why this feels faster than just using a `manpage` - maybe public shame will help me memorize this instead of just looking it up always.`

```
useradd --create-home --groups sudo,adm $USER

`sudo usermod -a -G dialout $(whoami)`
`sudo usermod -a -G dialout,plugdev $(whoami)`
```

```
# For Switch Homebrew UDEV Rules:
`sudo usermod -a -G nintendo_switch $USER`
```

`https://wiki.archlinux.org/title/Users_and_groups#User_management`

# Manjaro
`sudo useradd -m -G tty,libvirt,uucp,wheel,dialout -s /bin/zsh $USER`
