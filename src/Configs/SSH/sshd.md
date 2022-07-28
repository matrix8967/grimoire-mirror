# System SSH Daemon Config

* * *

Wisdom: `https://www.ssh.com/academy/ssh/sshd_config`

* * *

## Baseline SSHD Config:

```
Port $SSH_Port_Number
HostKey /etc/ssh/ssh_host_rsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key
SyslogFacility AUTHPRIV
AuthorizedKeysFile	.ssh/authorized_keys
PasswordAuthentication no
ChallengeResponseAuthentication no
GSSAPIAuthentication yes
GSSAPICleanupCredentials no
UsePAM yes
X11Forwarding no
# X11UseLocalhost no
Banner /etc/issue.net
AcceptEnv LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
AcceptEnv LC_IDENTIFICATION LC_ALL LANGUAGE
AcceptEnv XMODIFIERS
Subsystem	sftp	/usr/lib/openssh/sftp-server
PermitRootLogin no
```

* * *

### Bypass `2FA` for SSH User.

When `2FA` is enabled for SSH Logins - it maybe neccesary to exclude certain users from using `2FA` for Troubleshooting, Automation, or Recovery Purposes:

```
Match User $USER Address $IP_ADDRESS
       AuthenticationMethods publickey
```

* * *

### SFTP Jails:

**Note:** (This needs cleaning & updating.)

Using SSH to share files is a reasonably safe and low friction way to share files.

A basic SFTP Jail creates a dedicated User and Group that serves no other purpose than authenticating to a server to share files.

`sudo groupadd sftpjail`

- Create a new group for our SFTP Jail.

```bash
sudo useradd -g sftpjail -s /bin/false -m -d /home/$USER $USER
```

* Add a new user.
* Set the primary group to our `sftpjail` group.
* Set the login Shell to `false`.
* Set the `~/` directory to `/home/USERNAME`.
* Lastly: specify the username for the new user.

```bash
sudo passwd $USER
```

* Change the User's Password.

```bash
sudo chown root: /home/$USER
sudo chmod 755 /home/$USER
```
* Set permissions for the SFTP Jail.

```bash
sudo mkdir /home/$USER/uploads
sudo chmod 755 /home/$USER/uploads
sudo chown $USER:sftpjail /home/$USER/uploads
```
* Create an Upload Directory for the User.
* Set Permissions allowing the user to upload files.

#### Add/Edit your SSHD Config file to setup the default environment for users in the `sftpjail` group:

```
Subsystem sftp internal-sftp

Match Group sftpjail
   ChrootDirectory %h
   ForceCommand internal-sftp
   AllowTcpForwarding no
   X11Forwarding no
```

* * *
