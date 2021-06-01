<!-- Use `screen` or `minicom` instead of system's `shell` to interact with a `DB-9`/`rollover`/`console` cable. -->

# Screen

* `screen -dmLS session_name /dev/ttyUSB0 115200,cs8`
  - `-d` -- detatch session.
  - `-m` -- create new session.
  - `-L` -- safe updating of background session.
  - `-S` -- specify a session name.
* `screen -ls`
  - `ls` -- lists all screen sessions.
* `screen -r session_name`
  - `-r` -- reattach to a screen session.
* `screen -X -S session_name quit`
  - `-X` -- Execute a command on a session.

# Minicom

* `sudo usermod -a -G dialout $(whoami)`
  - Users must be added to the `dialout` user group.

* `minicom -c on -C ~/minicom.log`
  - `-c` Color Output Toggle.
  - `-C file_path.log` Capture a log of the session to the specified file path.

Either `minicom` or `screen` can be used to interact with equipment over a `DB-9` Cable.

The specific settings to establish a connection with [most] Ubitiquiti equipment is below.

```
    Baud rate: 115200
    Data bits: 8
    Parity: NONE
    Stop bits: 1
    Flow control: NONE
```
