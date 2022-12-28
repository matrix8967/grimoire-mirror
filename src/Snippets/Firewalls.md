# Firewalls

# `UFW`

## Allow on Interface

`sudo ufw allow in on $INTERFACE_NAME to any port 443`

## Allowing subnets:

`sudo ufw allow from 10.100.100.0/24 to any port 443`

## Delete Multiple Rules:

`sudo ufw status numbered`

`for i in 26 25 24 23 18 17 16 15 14 11 10 9 8; do sudo ufw delete $i;done`

(☝️ Be sure to list rules in reverse order to avoid reordering.)

## Tailscale Rules

```
sudo ufw allow in on tailscale0
sudo ufw allow 41641/udp
```

-----

# `firewalld` / `firewall-cmd`

```bash
sudo semanage port -a -t ssh_port_t -p tcp 8967
sudo firewall-cmd --add-port=8967/tcp --permanent
sudo firewall-cmd --reload
```

----

# To-Do:

* `iptables`
* 