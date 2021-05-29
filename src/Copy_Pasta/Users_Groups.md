# Users & Groups copypasta.

# Good starting point for adding a user on *nix system/server.
`useradd --create-home --groups sudo,adm $USER`

---

# Modifying an existing user's group memberships.

`sudo usermod -a -G dialout,plugdev $(whoami)`

---

# Manjaro one-liner for setting default groups (Arch's `UUCP`) & setting the login shell.
# `https://wiki.archlinux.org/title/Users_and_groups#User_management`

`sudo useradd -m -G tty,libvirt,uucp,wheel,dialout -s /bin/zsh $USER`

---

# Homebrew Switch `udev` rules to allow running `nvidia tegra exploit` code w/o `root`

`sudo usermod -a -G nintendo_switch $USER`
