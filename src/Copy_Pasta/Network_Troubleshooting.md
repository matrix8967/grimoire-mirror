# Network_Troubleshooting

## Netstat

`sudo netstat -tlnp`

-   `t` = `tcp`

-   `l` = `listening sockets`

-   `n` = `do not resolve dns to hostnames`

-   `p` = `show process id`

* * *

## DB9 Serial Cable Recovery:

### Screen

-   `screen -dmLS session_name /dev/ttyUSB0 115200,cs8`
    -   `-d` -- detatch session.
    -   `-m` -- create new session.
    -   `-L` -- safe updating of background session.
    -   `-S` -- specify a session name.
-   `screen -ls`
    -   `ls` -- lists all screen sessions.
-   `screen -r session_name`
    -   `-r` -- reattach to a screen session.
-   `screen -X -S session_name quit`
    -   `-X` -- Execute a command on a session.

### Minicom

-   `sudo usermod -a -G dialout $(whoami)`

    -   Users must be added to the `dialout` user group.

-   `minicom -c on -C ~/minicom.log`
    -   `-c` Color Output Toggle.
    -   `-C file_path.log` Capture a log of the session to the specified file path.

Either `minicom` or `screen` can be used to interact with equipment over a `DB-9` Cable.

* * *

### Edgerouter / Edgeswitch Serial Config

The specific settings to establish a connection with most Ubitiquiti equipment is below.

        Baud rate: 115200
        Data bits: 8
        Parity: NONE
        Stop bits: 1
        Flow control: NONE

* * *

## OSI Model

1.  Please (Physical)
2.  Do (Data Link)
3.  Not (Network)
4.  Throw (Transport)
5.  Sausage (Session)
6.  Pizza (Presentation)
7.  Away (Application)

* * *

## CIDR Notation

A way of defining a subnet and its size with a "mask", a smaller mask = more address bits usable by the subnet & more IPs in the range. Most common ones:

    10.0.0.1/32 (a single IP address, 10.0.0.1) netmask = 255.255.255.255
    10.0.0.1/24 (255 ips from 10.0.0.1-255) netmask = 255.255.255.0
    10.0.0.1/16 (65,536 ips from 10.0.0.0 - 10.0.255.255) netmask = 255.255.0.0
    10.0.0.1/8 (16,777,216 ips from 10.0.0.0 - 10.255.255.255) netmask = 255.0.0.0
    0.0.0.1/0 (4,294,967,296 ips from 0.0.0.0 - 255.255.255.255) netmask = 0.0.0.0

        CIDR |  Hosts | Netmask
    -----------------------------------
        /30     4       255.255.255.252
        /29     8       255.255.255.248
        /28     16      255.255.255.240
        /27     32      255.255.255.224
        /26     64      255.255.255.192
        /25     128     255.255.255.128
        /24     256     255.255.255.0
        /23     512     255.255.254.0
        /22     1024    255.255.252.0
        /21     2048    255.255.248.0
        /20     4096    255.255.240.0
        /19     8192    255.255.224.0
        /18     16384   255.255.192.0
        /17     32768   255.255.128.0
        /16     65536   255.255.0.0

On most `*nix` OS - the packages `ipcalc` and `sipcalc` make for a quick-and-dirty subnet calculator.
