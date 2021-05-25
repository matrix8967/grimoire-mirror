# User Doc -

## SSH Components - Local & Remote

## Asciinema Capture & Upload

## Ideal 5-layer SSH Beandip:

* No Passwords for anyone, ever. Only Keypairs.
    * Don't acknowledge `root` login attempts.
* Changing the Default Port.
* Fail2Ban
* 2FA

## Recovery Options:

* Running a new detached `ssh` session on an adjacent port. `/usr/sbin/sshd -D -p 2222`
* Bringing down an `EC2` Instance, Disconnecting the `rootfs`, mounting the `rootfs` to another `EC2`, etc.

## Future Work & Improvements:

* Ephemeral Bastion Hosts with terminal recording.
* SSH-CA to centralize key mgmt.
* Legal Compliance MOTD that does _nothing_ except make lawyers happy.

---

# Intro
# SSH Keygen / Matching Keypairs / Future Work.
# Components
# Common Failures
# Recovery / Break-Glass
# Vocab
# TODO / Refs

---

# SSH TODO / Research:

- `sftp` & other storage use cases.
	+ `rsync +ssh`

# Misc SSH Stuff

- SSH Certificate Authority
	+ This will allow for better SSH Key Rotation(s).

- Bastion hosts:
	+ Ideally: a temporary logged & auth'd `ssh` work flow.

- SSH Recovery for manipulating `sshd.conf`
	+ new `ssh session`
	+ killing an instance & mounting it to a new `ec2` instance as a block device.
- Notes on `~/.bashrc` and how it will fuck you up.
- SSH Forwarding

----


`ssh-keygen -t rsa -b 4096 -C "user@garyhost" -f ~/.ssh/example_01`

`ssh-copy-id -i ~/.ssh/example_01.pub`
