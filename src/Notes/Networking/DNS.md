# DNS

-----

# TL;DR Troubleshooting:

-   `ping www.google.com`

-   `ping 8.8.8.8`
    -   Did `8.8.8.8` return results -- but using the _domain name_ `www.google.com` return errors? Congrats! You've got `DNS` issues!

-   Can you ping some rando website you've not visited before now? (lookin' at you `yahoo.com`)

-   Does the issue persist if you connect to a VPN, Mobile Hotspot, or use your 4G/5G Connection from your phone while your Wireless is turned off?

-   Is the issue different in a different browser?
    -   Does the issue persist in an Incognito Session?

### `dig`

-   `dig +short heretic.dev`
    		\- Returns DNS Query output, minimal spam.

-   `dig +trace +short heretic.dev`
    		\- Returns DNS Results for each path taken en route to the host.

-   `dig +short @8.8.8.8 heretic.dev`
    		\- Specifies an alternative DNS Server for queries.

### `nslookup`

-   `nslookup heretic.dev`

-   `nslookup -debug heretic.dev`

-   `nslookup -debug heretic.dev 8.8.8.8`

### `host`

-   `host heretic.dev`

-   `host heretic.dev 8.8.8.8`

## Misc

-   Change the local DNS to a different DNS Server.
    -   Here's a quick and dirty list of some public DNS Servers you can use to troubleshoot:

### IPv4:

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

### IPv6: Don't touch it. But if you have to:

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

-----

## A crash course in DNS:

-   DNS (Domain Name System) translates your device(s) human readable `hostname` into a machine readable `IP Address.`
-   Every networked device, no matter how small, interacts with DNS in some way.
-   If you're reading this - something is probably interacting with DNS in a negative way.

## Bottoms Up 🍻

-   Start from the bottom, and work your way up.
    -   (Remember Drake? 😬️)

-   A general rule for systems during a conflict: _Whatever's closest to the user wins..._
    - This is to say if there's a conflict in `DNS`, or _almost ANY_ network wide configuration, the machine will defer to what it knows to be _the most_ true
    - ...which is itself.
      - "Always conduct yourself with the confidence of your laptop's `DNS Resolver` during outages." -

## _`localhost` will remember that..._

-   Your local device (laptop, phone, the espresso machine, whatever) all have a built in `DNS Resolver`. It listens on a `loopback` address which by default is `127.0.0.1` on most systems and assigns itself the name `localhost.`

-   If you interact with `heretic.dev` your local DNS will go out onto the mean streets of the internet, fetch the IP Address of the server that hosts the domain, and take you there. To avoid unnecessary trips your local DNS will remember the DNS Record for you so that it doesn't have to go ask mom and dad where to find it.

-   If this address changes - your machine will _SHOULD_ go out and fetch the new address for you. But - if it's been less than ~24 hours, most DNS servers will assume there hasn't been a dramatic change and serve you a `stale record`.
