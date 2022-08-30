# EdgeRouter

## Misc EdgeRouter Commands:

-   `terminal length 0`
    -   Removes default CLI paging limit.

## Sanitize Configs:

Shell Function to strip `RFC1918` IP Ranges (Private IPs/Subnets) from config files before uploading.

```bash

function Strip_IPs {
	sed -E -r 's/(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)/$IP_ADDRESSES/g' $1
}

```

### Usage:

`Strip_IPs $filename.conf` - displays sanitized `filename.conf.` Save to new file with `>` shell operand.

* * *

## Adding Debian Package Repos:

```bash
configure
set system package repository stretch components 'main contrib non-free'
set system package repository stretch distribution stretch
set system package repository stretch url http://http.us.debian.org/debian
commit ; save
sudo apt-get update
```
-   ☝️ *DO NOT* use `sudo apt-get upgrade`

See for details:
`https://help.ui.com/hc/en-us/articles/205202560-EdgeRouter-Add-Debian-Packages-to-EdgeOS`
