# SystemD

-----

# `systemd`

> `systemd-analyze`
* Display process startup time:

> `systemd-analyze blame`
* Display process startup time at service level:

> `/etc/systemd/system`
> `/usr/lib/systemd/system`
* Unit file locations.

-----

# `systemctl`

> `systemctl list-units`
* List running units:

> `systemctl status`
* List system status:

> `systemctl --failed`
* List failed services

> `systemctl list-units`
* List all loaded/active units

> `systemctl list-units --state=running`
* List running units

> `systemctl status foo`
* Check the status of a service

> `systemctl {start,stop,restart,reload} foo`
* Control a service

> `systemctl {enable,disable} foo`
* Change startup on boot

> `systemctl list-dependencies foo.service`
* List the dependencies of a service
* when no service name is specified, lists the dependencies of default.target

> `systemd-analyze blame`
* Show boot chain

-----

# `journalctl`

> `journalctl -f`
* actively follow log (like tail -f):

> `journalctl -b -p err`
* display all errors since last boot:

> `journalctl --since=2012-10-15 --until="2011-10-16 23:59:59"`
* filter by time period:

> `journalctl -F _SYSTEMD_UNIT`
* show list of systemd units logged in journal:

> `journalctl -u dbus`
* filter by specific unit:

> `journalctl /usr/bin/dbus-daemon`
* filter by executable name:

> `journalctl _PID=123`
* filter by PID:

> `journalctl _COMM=sshd`
* filter by Command, e.g., sshd:

> `journalctl _COMM=crond --since '10:00' --until '11:00'`
* filter by Command and time period:

> `journalctl --list-boots`
* list all available boots:

> `journalctl _UID=1000`
* filter by specific User ID e.g., user id 1000:

> `journalctl --disk-usage`
* display the current disk usage of all journal files: