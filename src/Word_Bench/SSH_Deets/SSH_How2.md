# SSH

`ssh` is a network protocol used to provide secure services on a presumably insecure network. It's most common use case is to provide a `s`ecure `sh`ell without fear of the network traffic being intercepted in transit. However, it has _many_ other practical uses outside of this.

The role `ssh` plays at Apptegy, (and around the world) show no signs of becoming obsolete, so it's worth codifying some of our own "best practices" and common pitfalls.

---

# SSH Keypairs

A _minimal_ baseline for a remote host is to accept a cryptographic keypair (instead of, or along side) a password.

The nuances of Symmetric Key Crypto, Diffie-Hellman Elyptical Curves, Hashing, and all the _fun stuff_ are out of scope for this doc. :(

## Creating Public/Private Keys w/ `ssh-keygen`

Creating a keypair is done by using the `ssh-keygen` command. By default - this will prompt the user for some information while providing some pretty sane defaults.

The default private key file is located at `~/.id_rsa` and the default public key is located at `~/id_rsa.pub`.

It's likely Apptegy's SSH-Users will be using multiple keys

We're going to ignore the defaults for now, and create the key by specifying the exact key location, and the `comment` section of the key:

`ssh-keygen -t rsa -b 4096 -C "user@hostname_example" -f ~/.ssh/example_01`

This creates two files in `~/.ssh/`
* `example_01` - Private Key.
* `example_01.pub` - Public Key.

Once our keypair is created, we need to make sure the remote host is aware of our public key.

## Sharing Keys

To initiate a key exchange, we use the `ssh-copy-id` command, while specifying our `Identity File` - which for us is our public key.

`ssh-copy-id -i ~/.ssh/example_01.pub`

The remote host will prompt for another authentication method, and once accepted, will add the contents of our `example_01.pub` file to `~/.authorized_keys`.

## Passphrases on Keys

- Apptegy Client SSH Keypairs should be generated without a passphrase.
- Keys for automation should be generated without a passphrase for now.
    + Once Automation is in better shape, we can modify the `sshd` to accept the keypair without prompting for the passphrase. 01-22-20 -AM.
- User Auth Keys should be generated _with_ a passphrase.
	+ Passphrase can/should be stored in the user's `keychain` of whatever OS they're using.


---

# Current WIP / TODO from the DevOps Team:

The 7-layer bean-dip of SSH Authentication looks like this:

* No Passwords for anyone, ever. Only Keypairs.
    * Don't acknowledge `root` login attempts.
* Changing the Default Port.
* Fail2Ban
* 2FA
* Bastion Host(s) with session logging
* Creating an SSH Certificate Authority to centralize & automate keypairs.
* Adding things like a `MOTD` banner will make lawyers happy as well.

---

# Recovery/Break Glass of remote hosts.

* `/usr/sbin/sshd -D -p 2222` --> This will spawn a new SSH Daemon Process on the specified port to act as a recovery in case a remote shell is terminated, so long as the parent process stays alive.

* Absolute Break Glass (modifying broken `sshd.conf`, etc.)
    + Bring down `EC2` Instance,
    + Disconnect the `rootfs`
    + Mount the `rootfs` to another `EC2`.
    + Edit what you need. Follow steps in reverse.

---
