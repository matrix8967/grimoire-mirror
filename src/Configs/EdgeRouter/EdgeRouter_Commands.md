# EdgeRouter
```bash,editable
set firewall all-ping enable
set firewall broadcast-ping disable
set firewall group network-group LAN_NETWORKS description 'RFC1918 ranges'
set firewall group network-group LAN_NETWORKS network $IP_ADDRESSES/16
set firewall group network-group LAN_NETWORKS network $IP_ADDRESSES/12
set firewall group network-group LAN_NETWORKS network $IP_ADDRESSES/8
set firewall ipv6-name WANv6_IN default-action drop
set firewall ipv6-name WANv6_IN description 'WAN inbound traffic forwarded to LAN'
set firewall ipv6-name WANv6_IN enable-default-log
set firewall ipv6-name WANv6_IN rule 10 action accept
set firewall ipv6-name WANv6_IN rule 10 description 'Allow established/related sessions'
set firewall ipv6-name WANv6_IN rule 10 state established enable
set firewall ipv6-name WANv6_IN rule 10 state related enable
set firewall ipv6-name WANv6_IN rule 20 action drop
set firewall ipv6-name WANv6_IN rule 20 description 'Drop invalid state'
set firewall ipv6-name WANv6_IN rule 20 state invalid enable
set firewall ipv6-name WANv6_LOCAL default-action drop
set firewall ipv6-name WANv6_LOCAL description 'WAN inbound traffic to the router'
set firewall ipv6-name WANv6_LOCAL enable-default-log
set firewall ipv6-name WANv6_LOCAL rule 10 action accept
set firewall ipv6-name WANv6_LOCAL rule 10 description 'Allow established/related sessions'
set firewall ipv6-name WANv6_LOCAL rule 10 state established enable
set firewall ipv6-name WANv6_LOCAL rule 10 state related enable
set firewall ipv6-name WANv6_LOCAL rule 20 action drop
set firewall ipv6-name WANv6_LOCAL rule 20 description 'Drop invalid state'
set firewall ipv6-name WANv6_LOCAL rule 20 state invalid enable
set firewall ipv6-name WANv6_LOCAL rule 30 action accept
set firewall ipv6-name WANv6_LOCAL rule 30 description 'Allow IPv6 icmp'
set firewall ipv6-name WANv6_LOCAL rule 30 protocol ipv6-icmp
set firewall ipv6-name WANv6_LOCAL rule 40 action accept
set firewall ipv6-name WANv6_LOCAL rule 40 description 'allow dhcpv6'
set firewall ipv6-name WANv6_LOCAL rule 40 destination port 546
set firewall ipv6-name WANv6_LOCAL rule 40 protocol udp
set firewall ipv6-name WANv6_LOCAL rule 40 source port 547
set firewall ipv6-receive-redirects disable
set firewall ipv6-src-route disable
set firewall ip-src-route disable
set firewall log-martians enable
set firewall name GUEST_IN default-action accept
set firewall name GUEST_IN description 'guest to lan/wan'
set firewall name GUEST_IN rule 20 action drop
set firewall name GUEST_IN rule 20 description 'drop guest to lan'
set firewall name GUEST_IN rule 20 destination group network-group LAN_NETWORKS
set firewall name GUEST_IN rule 20 protocol all
set firewall name GUEST_LOCAL default-action drop
set firewall name GUEST_LOCAL description 'guest to router'
set firewall name GUEST_LOCAL rule 10 action accept
set firewall name GUEST_LOCAL rule 10 description 'allow dns'
set firewall name GUEST_LOCAL rule 10 destination port 53
set firewall name GUEST_LOCAL rule 10 log disable
set firewall name GUEST_LOCAL rule 10 protocol tcp_udp
set firewall name GUEST_LOCAL rule 20 action accept
set firewall name GUEST_LOCAL rule 20 description 'allow dhcp'
set firewall name GUEST_LOCAL rule 20 destination port 67
set firewall name GUEST_LOCAL rule 20 log disable
set firewall name GUEST_LOCAL rule 20 protocol udp
set firewall name WAN_IN default-action drop
set firewall name WAN_IN description 'WAN to internal'
set firewall name WAN_IN rule 10 action accept
set firewall name WAN_IN rule 10 description 'Allow established/related'
set firewall name WAN_IN rule 10 state established enable
set firewall name WAN_IN rule 10 state related enable
set firewall name WAN_IN rule 20 action drop
set firewall name WAN_IN rule 20 description 'Drop invalid state'
set firewall name WAN_IN rule 20 state invalid enable
set firewall name WAN_LOCAL default-action drop
set firewall name WAN_LOCAL description 'WAN to router'
set firewall name WAN_LOCAL rule 10 action accept
set firewall name WAN_LOCAL rule 10 description 'Allow established/related'
set firewall name WAN_LOCAL rule 10 state established enable
set firewall name WAN_LOCAL rule 10 state related enable
set firewall name WAN_LOCAL rule 20 action drop
set firewall name WAN_LOCAL rule 20 description 'Drop invalid state'
set firewall name WAN_LOCAL rule 20 state invalid enable
set firewall receive-redirects disable
set firewall send-redirects enable
set firewall source-validation disable
set firewall syn-cookies enable
set interfaces ethernet eth0 address dhcp
set interfaces ethernet eth0 description cyberspace
set interfaces ethernet eth0 duplex auto
set interfaces ethernet eth0 firewall in ipv6-name WANv6_IN
set interfaces ethernet eth0 firewall in name WAN_IN
set interfaces ethernet eth0 firewall local ipv6-name WANv6_LOCAL
set interfaces ethernet eth0 firewall local name WAN_LOCAL
set interfaces ethernet eth0 speed auto
set interfaces ethernet eth1 duplex auto
set interfaces ethernet eth1 speed auto
set interfaces ethernet eth2 duplex auto
set interfaces ethernet eth2 speed auto
set interfaces ethernet eth3 duplex auto
set interfaces ethernet eth3 speed auto
set interfaces ethernet eth4 duplex auto
set interfaces ethernet eth4 speed auto
set interfaces ethernet eth5 duplex auto
set interfaces ethernet eth5 speed auto
set interfaces ethernet eth6 duplex auto
set interfaces ethernet eth6 speed auto
set interfaces ethernet eth7 address $IP_ADDRESSES/24
set interfaces ethernet eth7 description LAN
set interfaces ethernet eth7 duplex auto
set interfaces ethernet eth7 mtu 1500
set interfaces ethernet eth7 speed auto
set interfaces ethernet eth7 vif 20 address $IP_ADDRESSES/24
set interfaces ethernet eth7 vif 20 description IOT
set interfaces ethernet eth7 vif 20 firewall in name GUEST_IN
set interfaces ethernet eth7 vif 20 firewall local name GUEST_LOCAL
set interfaces ethernet eth7 vif 666 address $IP_ADDRESSES/16
set interfaces ethernet eth7 vif 666 description heck
set interfaces ethernet eth7 vif 666 firewall in name GUEST_IN
set interfaces ethernet eth7 vif 666 firewall local name GUEST_LOCAL
set interfaces loopback lo
set port-forward auto-firewall enable
set port-forward hairpin-nat enable
set port-forward lan-interface eth7
set port-forward lan-interface eth7.20
set port-forward lan-interface eth7.666
set port-forward wan-interface eth0
set service dhcp-server disabled false
set service dhcp-server hostfile-update disable
set service dhcp-server shared-network-name IOT authoritative disable
set service dhcp-server shared-network-name IOT subnet $IP_ADDRESSES/24 default-router $IP_ADDRESSES
set service dhcp-server shared-network-name IOT subnet $IP_ADDRESSES/24 dns-server $IP_ADDRESSES
set service dhcp-server shared-network-name IOT subnet $IP_ADDRESSES/24 dns-server $IP_ADDRESSES
set service dhcp-server shared-network-name IOT subnet $IP_ADDRESSES/24 lease 86400
set service dhcp-server shared-network-name IOT subnet $IP_ADDRESSES/24 start $IP_ADDRESSES stop $IP_ADDRESSES
set service dhcp-server shared-network-name heck authoritative disable
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 default-router $IP_ADDRESSES
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 dns-server $IP_ADDRESSES
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 dns-server $IP_ADDRESSES
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 lease 86400
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 start $IP_ADDRESSES stop $IP_ADDRESSES
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 static-mapping deadsea ip-address $IP_ADDRESSES
set service dhcp-server shared-network-name heck subnet $IP_ADDRESSES/16 static-mapping deadsea mac-address '$MAC-ADDRESS'
set service dhcp-server static-arp disable
set service dhcp-server use-dnsmasq disable
set service dns forwarding cache-size 150
set service dns forwarding listen-on eth7
set service dns forwarding listen-on eth7.666
set service dns forwarding listen-on eth7.20
set service gui http-port 80
set service gui https-port 443
set service gui listen-address $IP_ADDRESSES
set service gui older-ciphers enable
set service nat rule 5010 description 'masquerade for WAN'
set service nat rule 5010 outbound-interface eth0
set service nat rule 5010 type masquerade
set service ssh disable-password-authentication
set service ssh listen-address $IP_ADDRESSES
set service ssh port 8967
set service ssh protocol-version v2
set service ubnt-discover disable
set service ubnt-discover-server disable
set service unms disable
set system analytics-handler send-analytics-report false
set system crash-handler send-crash-report false
set system domain-name $DOMAIN
set system host-name $ROUTER-HOSTNAME
set system login user matrix authentication encrypted-password '$ENCRYPTED_PASSWORD'
set system login user matrix authentication public-keys $USER@$HOSTNAME key $PUBLIC-KEY
set system login user matrix authentication public-keys $USER@HOSTNAME type ssh-rsa
set system login user matrix level admin
set system name-server $IP_ADDRESSES
set system ntp server 0.debian.pool.ntp.org prefer
set system ntp server 0.ubnt.pool.ntp.org
set system ntp server 1.debian.pool.ntp.org
set system ntp server 1.ubnt.pool.ntp.org
set system ntp server 2.debian.pool.ntp.org
set system ntp server 2.ubnt.pool.ntp.org
set system ntp server 3.debian.pool.ntp.org
set system ntp server 3.ubnt.pool.ntp.org
set system package repository stretch components 'main contrib non-free'
set system package repository stretch distribution stretch
set system package repository stretch password ''
set system package repository stretch url 'http://http.us.debian.org/debian'
set system package repository stretch username ''
set system syslog console facility syslog level info
set system syslog global facility all level notice
set system syslog global facility protocols level debug
set system syslog host $IP_ADDRESSES facility all level warning
set system time-zone America/Chicago
set system traffic-analysis dpi enable
set system traffic-analysis export enable
set traffic-control optimized-queue policy global
set traffic-control optimized-queue policy queues
```
