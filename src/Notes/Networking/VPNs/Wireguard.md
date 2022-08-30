# Wireguard

-----

# Map

<object type="image/svg+xml" data="../../../Images/Proxy_Map.svg" width="1024" height="768">></object>

-----

# ASCII Maps:

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