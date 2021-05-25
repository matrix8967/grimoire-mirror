* Use `screen` or `minicom` instead of a general `tty` to interact with a `DB-9`/`rollover` cable.

# Screen

`screen /dev/ttyUSB0 115200,cs8`
`screen -dmLS session_name /dev/ttyUSB0 115200,cs8`
`screen -ls`
`screen -r session_name`
`screen -X -S session_name quit`

    Baud rate: 115200
    Data bits: 8
    Parity: NONE
    Stop bits: 1
    Flow control: NONE

# Minicom

`sudo usermod -a -G dialout $(whoami)`
`minicom -c on -C ~/minicom.log`

## catch `stdout/stderr`
`sudo cat /dev/ttyUSB0 > output.log`

## Serial USB Info
`udevadm info -a -p  $(udevadm info -q path -n /dev/ttyUSB0)`
