# EdgeRouter

* * *

The default config output for `VyOS` routers is a `json` config file that can be restored from backup via the `CLI`, `WebUI` or from a [Recovery Console](../../Configs/Terminal/Minicom.md) with a [`DB-9/Rollover`](../../Snippets/Network_Troubleshooting.md#db9-serial-cable-recovery) cable if you're having an especially bad time.

Again, this is my default `VyOS` router config with production data replaced with `$VARIABLES`.

* * *

```json,editable
firewall {
    all-ping enable
    broadcast-ping disable
    group {
        network-group LAN_NETWORKS {
            description "RFC1918 ranges"
            network $IP_ADDRESSES/16
            network $IP_ADDRESSES/12
            network $IP_ADDRESSES/8
        }
    }
    ipv6-name WANv6_IN {
        default-action drop
        description "WAN inbound traffic forwarded to LAN"
        enable-default-log
        rule 10 {
            action accept
            description "Allow established/related sessions"
            state {
                established enable
                related enable
            }
        }
        rule 20 {
            action drop
            description "Drop invalid state"
            state {
                invalid enable
            }
        }
    }
    ipv6-name WANv6_LOCAL {
        default-action drop
        description "WAN inbound traffic to the router"
        enable-default-log
        rule 10 {
            action accept
            description "Allow established/related sessions"
            state {
                established enable
                related enable
            }
        }
        rule 20 {
            action drop
            description "Drop invalid state"
            state {
                invalid enable
            }
        }
        rule 30 {
            action accept
            description "Allow IPv6 icmp"
            protocol ipv6-icmp
        }
        rule 40 {
            action accept
            description "allow dhcpv6"
            destination {
                port 546
            }
            protocol udp
            source {
                port 547
            }
        }
    }
    ipv6-receive-redirects disable
    ipv6-src-route disable
    ip-src-route disable
    log-martians enable
    name GUEST_IN {
        default-action accept
        description "guest to lan/wan"
        rule 20 {
            action drop
            description "drop guest to lan"
            destination {
                group {
                    network-group LAN_NETWORKS
                }
            }
            protocol all
        }
    }
    name GUEST_LOCAL {
        default-action drop
        description "guest to router"
        rule 10 {
            action accept
            description "allow dns"
            destination {
                port 53
            }
            log disable
            protocol tcp_udp
        }
        rule 20 {
            action accept
            description "allow dhcp"
            destination {
                port 67
            }
            log disable
            protocol udp
        }
    }
    name WAN_IN {
        default-action drop
        description "WAN to internal"
        rule 10 {
            action accept
            description "Allow established/related"
            state {
                established enable
                related enable
            }
        }
        rule 20 {
            action drop
            description "Drop invalid state"
            state {
                invalid enable
            }
        }
    }
    name WAN_LOCAL {
        default-action drop
        description "WAN to router"
        rule 10 {
            action accept
            description "Allow established/related"
            state {
                established enable
                related enable
            }
        }
        rule 20 {
            action drop
            description "Drop invalid state"
            state {
                invalid enable
            }
        }
    }
    receive-redirects disable
    send-redirects enable
    source-validation disable
    syn-cookies enable
}
interfaces {
    ethernet eth0 {
        address dhcp
        description cyberspace
        duplex auto
        firewall {
            in {
                ipv6-name WANv6_IN
                name WAN_IN
            }
            local {
                ipv6-name WANv6_LOCAL
                name WAN_LOCAL
            }
        }
        speed auto
    }
    ethernet eth1 {
        duplex auto
        speed auto
    }
    ethernet eth2 {
        duplex auto
        speed auto
    }
    ethernet eth3 {
        duplex auto
        speed auto
    }
    ethernet eth4 {
        duplex auto
        speed auto
    }
    ethernet eth5 {
        duplex auto
        speed auto
    }
    ethernet eth6 {
        duplex auto
        speed auto
    }
    ethernet eth7 {
        address $IP_ADDRESSES/24
        description LAN
        duplex auto
        mtu 1500
        speed auto
        vif 20 {
            address $IP_ADDRESSES/24
            description IOT
            firewall {
                in {
                    name GUEST_IN
                }
                local {
                    name GUEST_LOCAL
                }
            }
        }
        vif 666 {
            address $IP_ADDRESSES/16
            description heck
            firewall {
                in {
                    name GUEST_IN
                }
                local {
                    name GUEST_LOCAL
                }
            }
        }
    }
    loopback lo {
    }
}
port-forward {
    auto-firewall enable
    hairpin-nat enable
    lan-interface eth7
    lan-interface eth7.20
    lan-interface eth7.666
    wan-interface eth0
}
service {
    dhcp-server {
        disabled false
        hostfile-update disable
        shared-network-name IOT {
            authoritative disable
            subnet $IP_ADDRESSES/24 {
                default-router $IP_ADDRESSES
                dns-server $IP_ADDRESSES
                dns-server $IP_ADDRESSES
                lease 86400
                start $IP_ADDRESSES {
                    stop $IP_ADDRESSES
                }
            }
        }
        shared-network-name heck {
            authoritative disable
            subnet $IP_ADDRESSES/16 {
                default-router $IP_ADDRESSES
                dns-server $IP_ADDRESSES
                dns-server $IP_ADDRESSES
                lease 86400
                start $IP_ADDRESSES {
                    stop $IP_ADDRESSES
                }
                static-mapping deadsea {
                    ip-address $IP_ADDRESSES
                    mac-address $MAC_ADDRESS
                }
            }
        }
        static-arp disable
        use-dnsmasq disable
    }
    dns {
        forwarding {
            cache-size 150
            listen-on eth7
            listen-on eth7.666
            listen-on eth7.20
        }
    }
    gui {
        http-port 80
        https-port 443
        listen-address $IP_ADDRESSES
        older-ciphers enable
    }
    nat {
        rule 5010 {
            description "masquerade for WAN"
            outbound-interface eth0
            type masquerade
        }
    }
    ssh {
        disable-password-authentication
        listen-address $IP_ADDRESSES
        port $SSH-PORT
        protocol-version v2
    }
    ubnt-discover {
        disable
    }
    ubnt-discover-server {
        disable
    }
    unms {
        disable
    }
}
system {
    analytics-handler {
        send-analytics-report false
    }
    crash-handler {
        send-crash-report false
    }
    domain-name $DOMAIN
    host-name $ROUTER-HOSTNAME
    login {
        user $USER {
            authentication {
                encrypted-password ****************
                public-keys $USER@$HOST {
                    key ****************
                    type ssh-rsa
                }
            }
            level admin
        }
    }
    name-server $IP_ADDRESSES
    ntp {
        server 0.debian.pool.ntp.org {
            prefer
        }
        server 0.ubnt.pool.ntp.org {
        }
        server 1.debian.pool.ntp.org {
        }
        server 1.ubnt.pool.ntp.org {
        }
        server 2.debian.pool.ntp.org {
        }
        server 2.ubnt.pool.ntp.org {
        }
        server 3.debian.pool.ntp.org {
        }
        server 3.ubnt.pool.ntp.org {
        }
    }
    package {
        repository stretch {
            components "main contrib non-free"
            distribution stretch
            password ****************
            url http://http.us.debian.org/debian
            username ""
        }
    }
    syslog {
        console {
            facility syslog {
                level info
            }
        }
        global {
            facility all {
                level notice
            }
            facility protocols {
                level debug
            }
        }
        host $IP_ADDRESSES {
            facility all {
                level warning
            }
        }
    }
    time-zone America/Chicago
    traffic-analysis {
        dpi enable
        export enable
    }
}
traffic-control {
    optimized-queue {
        policy global
        policy queues
    }
}
```
