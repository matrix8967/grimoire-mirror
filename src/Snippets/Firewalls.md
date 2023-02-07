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

# Firewall-cmd

## Zone Info

```bash
sudo systemctl enable --now firewalld
sudo firewall-cmd --get-zones
sudo firewall-cmd --zone work --list-all
```

## Create Zones:

```bash
sudo firewall-cmd --new-zone corp --permanent
sudo firewall-cmd --reload
```

## Add SSH to new zone:

```bash
sudo firewall-cmd --zone corp --add-service ssh --permanent
```

## Change Interface(s):

```bash
firewall-cmd --change-interface ens3 \
  --zone corp --permanent
```

## Set Default Zone:

```bash
sudo firewall-cmd --set-default corp
```

## View Active Zones:

```bash
sudo firewall-cmd --get-active-zones
```

# Add/Remove Services:

```bash
sudo firewall-cmd --get-services

sudo systemctl --enable --now httpd

sudo firewall-cmd --add-service ssh --permanent
sudo firewall-cmd --reload

sudo firewall-cmd --remove-service ssh --permanent
sudo firewall-cmd --reload

sudo firewall-cmd --add-port 1622/tcp --permanent
sudo firewall-cmd --reload

sudo firewall-cmd --remove-port 1622/tcp --permanent
sudo firewall-cmd --reload
```

----

# To-Do:

* `iptables`