-----

# SSH

`sudo sshd -t`

* Test the `sshd_config` file for errors before reloading / restarting the service.

`/usr/sbin/sshd -D -p 2222`

* Create a new `ssh` instance in the foreground on a separate port as a failsafe shell. (like when editing `/etc/ssh/sshd_config`)

* Rsync + SSH

`rsync -azvhP -r -e ssh --info=progress2 /local/path/ /remote/path`

# Allow Keypair w/o 2FA in `/etc/sshd_config`

```
Match User $USER Address $IP_ADDRESS
       AuthenticationMethods publickey
```

-----
