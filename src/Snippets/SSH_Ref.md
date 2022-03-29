# SSH

### sshd

`sudo sshd -t`

-   Test the `sshd_config` file for errors before reloading / restarting the service.

`/usr/sbin/sshd -D -p 2222`

-   Create a new `ssh` instance in the foreground on a separate port as a failsafe shell. (like when editing `/etc/ssh/sshd_config`)

* * *

### 2FA for SSH

-   WIP

* * *

### Bypass `2FA` for SSH User.

#### `/etc/ssh/sshd_conf`

    Match User $USER Address $IP_ADDRESS
           AuthenticationMethods publickey

* * *
