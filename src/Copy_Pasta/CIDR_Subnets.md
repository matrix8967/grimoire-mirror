# CIDR Notation

A way of defining a subnet and its size with a "mask", a smaller mask = more address bits usable by the subnet & more IPs in the range. Most common ones:

    10.0.0.1/32 (a single IP address, 10.0.0.1) netmask = 255.255.255.255
    10.0.0.1/24 (255 ips from 10.0.0.1-255) netmask = 255.255.255.0
    10.0.0.1/16 (65,536 ips from 10.0.0.0 - 10.0.255.255) netmask = 255.255.0.0
    10.0.0.1/8 (16,777,216 ips from 10.0.0.0 - 10.255.255.255) netmask = 255.0.0.0
    0.0.0.1/0 (4,294,967,296 ips from 0.0.0.0 - 255.255.255.255) netmask = 0.0.0.0

# *nix packages for subnet math:
`sipcalc` // `ipcalc`


```
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
```
