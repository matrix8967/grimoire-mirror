# DNS

Start from your `localhost` (Desktop, Laptop, Phone, Espresso Machine, whatever) and work your way _up_ and _out_.

Continue moving _"up"_ the network layers to your gateway device/router, etc

-   `ping www.google.com`

-   `ping 8.8.8.8`

### dig

-   `dig +short $HOSTNAME`
    		\* Returns DNS Query output with minimal spam.

-   `dig +trace +short $HOSTNAME`
    		\* Returns DNS Results for each path taken en route to the host.

-   `dig +short @8.8.8.8 $HOSTNAME`
    		\* Specifies an alternative DNS Server for queries.

### nslookup

-   `nslookup $HOSTNAME`

-   `nslookup -debug $HOSTNAME`

-   `nslookup -debug $HOSTNAME 8.8.8.8`

### host

-   `host $HOSTNAME`

-   `host $HOSTNAME 8.8.8.8`

### Misc

Change the local DNS to a different DNS Server.

Here's a quick and dirty list of some public DNS Servers you can use to troubleshoot:

IPv4:

    Google DNS:
    8.8.8.8
    8.8.4.4

    Cloudflare:
    1.1.1.1
    1.0.0.1

    Quad9:
    9.9.9.9

    OpenDNS:
    208.67.222.222
    208.67.220.220

IPv6: Don't touch it. But if you have to:

    Google:
    2001:4860:4860::8888
    2001:4860:4860::8844

    Cloudflare:
    2606:4700:4700::1111
    2606:4700:4700::1001

    Quad9:
    2620:fe::fe

    OpenDNS:
    2620:0:ccc::2
    2620:0:ccd::2
