# Wireguard

## What is Wireguard?

WireGuard® is a modern and fast encrypted networking protocol that offers a number of performance benefits over traditional VPNs and TLS. Among other important features, WireGuard uses Curve25519 for key exchange, which keeps the negotiation phase extremely lightweight and fast. It also has a very low cost per live session, so it can keep direct connections open to a large number of nodes at once.

Here you can find a link to the original [Whitepaper](https://www.wireguard.com/papers/wireguard.pdf) as well as the source code for the [Linux Kernel Driver.](https://git.zx2c4.com/wireguard-linux/tree/drivers/net/wireguard/)

-----

## Keep-Alive & NAT-Traversal:

By default `Wireguard` is designed not to generate any unneccisary network traffic. However, many home & business networks rely on a technology called `NAT` to handle aspects of IP Addressing. This can cause `Wireguard` connections to be unstable if using the bare-bones configurations.

To configure `Wireguard` to send `Keepalive` packets, (thus preventing your network gateway from closing the connection) add the follwing to your Wireguard Configs:

`PersistentKeepAlive = 25`

## Limiting Subnets:

Rather than allowing `Wireguard` to manage *ALL* traffic on a network, it's useful to limit your `Wireguard` connection to a specific subnet:

`AllowedIPs = 10.10.10.0/24`

-----

### Maps

<object type="image/svg+xml" data="../../../Images/Proxy_Map.svg" width="1024" height="768">></object>

-----

### ASCII Maps:

A plaintext ASCII map for minimal documentation/reference.

```
#           ┌───────────┐
#           │    VPC    │
#           │           │
#           │ Wireguard │
#           │           │
#       ┌───┤   Caddy   ├────┐
#       │   └───────────┘    │VPN Tunnel
#       │                    │
# ┌─────┴────┐         ┌─────┴─────┐
# │   The    │         │           │
# │ Internet │         │  Gateway  │
# │   >:[    │         │           │
# │          │         │           │
# └──────────┘         └──┬──────┬─┘
#                         │      │
#                         │      │
#                         │      │
#                         │      │
#   ┌─┬─┬┬─┬─┐         ┌──┴──────┴─┐
#   ├─┘ └┘ └─┼─────────┤           │
#   │   VM   │   DMZ   │ Switch_01 │
#   │  Host  │  VLANs  │           │
#   ├─┐ ┌┐ ┌─┼─────────┤           │
#   └─┴─┴┴─┴─┘         └──┬────────┘
#                         │      ▲
#                         │      │
#                         │      │
#                         ▼      │
#                       ┌────────┴┐
#                       │ Trusted │
#                       │  Wired  │
#                       │  VLANs  │
#                       │         │
#                       └─────────┘
```