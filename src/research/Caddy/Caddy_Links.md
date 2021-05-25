# Caddy

https://geoff.tuxpup.com/posts/caddy_and_wireguard/
https://caddyserver.com/docs/caddyfile
https://caddyserver.com/docs/quick-starts/reverse-proxy
https://caddyserver.com/docs/

# /etc/caddy/Caddyfile

```
start.alexmorris.dev {
        reverse_proxy 45.33.127.233
        log {
                output file /var/log/caddy/start.alexmorris.dev.access.log {
                        roll_size 1gb
                        roll_keep 5
                        roll_keep_for 720h
                }
        }
}
```

# Caddy reverse_proxy

https://caddyserver.com/docs/quick-starts/reverse-proxy
https://caddyserver.com/docs/caddyfile/directives/reverse_proxy
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-For
https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-Proto

# Automatic HTTPS

https://caddyserver.com/docs/automatic-https
https://github.com/caddyserver/certmagic

# Logging

https://caddyserver.com/docs/logging
https://caddyserver.com/docs/metrics

# Misc
https://github.com/DoTheEvo/selfhosted-apps-docker/tree/master/caddy_v2
https://github.com/DoTheEvo/Traefik-v2-examples
( Same author of the Traefik guide )
