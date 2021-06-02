# Users & Groups copypasta.

`useradd --create-home --groups sudo,adm $USER`

	* Good starting point for adding a user on *nix system/server.

---

`sudo usermod -a -G dialout,plugdev $(whoami)`

	* Modifying an existing user's group memberships.

---

<!-- `https://wiki.archlinux.org/title/Users_and_groups#User_management` -->

`sudo useradd -m -G tty,libvirt,uucp,wheel,dialout -s /bin/zsh $USER`

	* Manjaro one-liner for setting default groups.

	* (Arch's `UUCP` & setting the login shell.)

---

`sudo usermod -a -G nintendo_switch $USER`

	* Homebrew Switch `udev` rules to allow running `nvidia tegra exploit` code w/o `root`
