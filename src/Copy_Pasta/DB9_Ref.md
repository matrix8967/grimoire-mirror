<!-- Use `screen` or `minicom` instead of system's `shell` to interact with a `DB-9`/`rollover`/`console` cable. -->

# Screen

`screen /dev/ttyUSB0 115200,cs8`
`screen -dmLS session_name /dev/ttyUSB0 115200,cs8`
`screen -ls`
`screen -r session_name`
`screen -X -S session_name quit`

# Minicom

`sudo usermod -a -G dialout $(whoami)`
`minicom -c on -C ~/minicom.log`

Either `minicom` or `screen` can be used to interact with equipment over a `DB-9` Cable.

The specific settings to establish a connection with [most] Ubitiquiti equipment is below.

```
    Baud rate: 115200
    Data bits: 8
    Parity: NONE
    Stop bits: 1
    Flow control: NONE
```
