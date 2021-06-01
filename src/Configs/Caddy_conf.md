# Caddy
### Reverse Proxy Redirection to Internal Site

`Caddy` is a powerful webserver that simplifies many of the most common usecases for other webservers like `nginx`.

Below is an example of a reverse proxy to an internal machine, while also logging to the `Caddy` host's local `log` directory.

```
$DOMAN-NAME {

        reverse_proxy $IP-OF-DESTINATION

        log {
                output file /var/log/caddy/$DOMAIN-NAME.access.log {
                        roll_size 1gb
                        roll_keep 5
                        roll_keep_for 720h
                }
        }
}
```
