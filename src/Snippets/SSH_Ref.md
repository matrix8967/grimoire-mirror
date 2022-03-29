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

### SSH Ref

-   `-4`  -- force ssh to use IPv4 addresses only.
-   `-6`  -- force ssh to use IPv6 addresses only.
-   `-a`  -- disable forwarding of authentication agent connection.
-   `-A`  -- enable forwarding of the authentication agent connection.
-   `-B`  -- bind to specified interface before attempting to connect.
-   `-b`  -- specify interface to transmit on.
-   `-C`  -- compress data.
-   `-c`  -- select encryption cipher.
-   `-D`  -- specify a dynamic port forwarding.
-   `-E`  -- append log output to file instead of stderr.
-   `-e`  -- set escape character.
-   `-f`  -- go to background.
-   `-F`  -- specify alternate config file.
-   `-g`  -- allow remote hosts to connect to local forwarded ports.
-   `-G`  -- output configuration and exit.
-   `-i`  -- select identity file.
-   `-I`  -- specify smartcard device.
-   `-J`  -- connect via a jump host.
-   `-k`  -- disable forwarding of GSSAPI credentials.
-   `-K`  -- enable GSSAPI-based authentication and forwarding.
-   `-L`  -- specify local port forwarding.
-   `-l`  -- specify login name.
-   `-M`  -- master mode for connection sharing.
-   `-m`  -- specify mac algorithms.
-   `-N`  -- don't execute a remote command.
-   `-n`  -- redirect stdin from /dev/null.
-   `-O`  -- control an active connection multiplexing master process.
-   `-o`  -- specify extra options.
-   `-p`  -- specify port on remote host.
-   `-P`  -- use non privileged port.
-   `-Q`  -- query parameters.
-   `-q`  -- quiet operation.
-   `-R`  -- specify remote port forwarding.
-   `-s`  -- invoke subsystem.
-   `-S`  -- specify location of control socket for connection sharing.
-   `-T`  -- disable pseudo-tty allocation.
-   `-t`  -- force pseudo-tty allocation.
-   `-V`  -- show version number.
-   `-v`  -- verbose mode (multiple increase verbosity, up to 3).
-   `-W`  -- forward standard input and output to host.
-   `-w`  -- request tunnel device forwarding.
-   `-x`  -- disable X11 forwarding.
-   `-X`  -- enable (untrusted) X11 forwarding.
-   `-Y`  -- enable trusted X11 forwarding.
-   `-y`  -- send log info via syslog instead of stderr.
