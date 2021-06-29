# SSH

### sshd

`sudo sshd -t`

-   Test the `sshd_config` file for errors before reloading / restarting the service.

`/usr/sbin/sshd -D -p 2222`

-   Create a new `ssh` instance in the foreground on a separate port as a failsafe shell. (like when editing `/etc/ssh/sshd_config`)

* * *

### Rsync

`rsync -rauLvhP`

-   `r` = Recursive
-   `a` = Archive
-   `z` = Compressed (zipped)
-   `u` = Ignore Unless Newer.
-   `L` = Preserve soft links.
-   `v` = verbose
-   `h` = Human Readable
-   `P` = Progress

* * *

### 2FA for SSH

-   WIP

* * *

### Bypass `2FA` for SSH User.

    Match User $USER Address $IP_ADDRESS
           AuthenticationMethods publickey

* * *
