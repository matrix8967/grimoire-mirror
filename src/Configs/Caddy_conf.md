```
$DOMAIN {

#	redir $DOMAIN{uri} {
	reverse_proxy $DOMAIN_URL {
		transport http {
			tls
			tls_insecure_skip_verify
		}
	}

        log {
                output file /var/log/caddy/$DOMAIN.access.log {
                        roll_size 1gb
                        roll_keep 5
                        roll_keep_for 720h
                }
        }
}
```

This super sucks - but can be useful for internal testing.

But still requires guilt and/or slut-shaming for not verifying certs. >:[