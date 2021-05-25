# SSH Components

## Remote Host System

`/etc/ssh/sshd.conf` - This is the core configuration for the `ssh server`. In an ideal world, nobody would ever need to manipulate this file on a remote server, and any changes could be peer reviewed in a repo.

Until then - if you find yourself needing to make an adjustment to this file, you should reflect _heavily_ on life choices that brought you to this moment. Whatever changes are being made should not be made in a vacuum. _However_ "abstinence only" is bad security posture, so I've included some safety checks to help mitigate risks of an `ssh` failure later in this article.

`/etc/ssh/ssh.conf` - This is the core configuration for the `ssh client` which is only interesting on an `ssh server` if we're using a Bastion Host or Proxy.

`~/.ssh/authorized_keys` - This file contains a list of `Public Keys` the server will accept.

## Your Local Client

`/etc/ssh/sshd.conf` - This is the core configuration for the `ssh server` which is only interesting on an `ssh client` if you're like me and will `ssh` into your work machine from across the room.

`/etc/ssh/ssh.conf` - This is the core configuration for the `ssh client` and it determines the defaults for how your client will approach an `ssh server`. This is where you can specify things like your default port, default keypairs, `X11 Forwarding` and lots of other things that may cause you grief if you deviate from sane defaults.

`~/.ssh/config` - This file contains host-specific changes. For example, if you maintain a system that uses a different port number or hashing algorithm, you can specify those here to avoid fumbling with terminal history and other hacky tricks.

----

# Vocab - Word Bank

* `Client` - The device you're using to reach out and establish a connection with a remote host. Likely your laptop, or some kind of proxy a.k.a "Bastion Host."

* `Host` - This is the machine you're connecting *to* from your client.

* `Keypair` - This is a set of two or more cryptographic keys that are created and exchanged in order to provide  cryptographic authentication to systems. Another common use for these keypairs is _finding the least fun person at a party_ - or so I've been told.

* `Public Key` - A Public Key is one-half of our keypair, and as the name suggests it's the half that is shared with the remote Host. The Host uses it as at least one authentication mechanism to check against the Private Key.

* `Private Key` - The Private key is the half that should only live on your client machine or encrypted in a trusted secrets manager.

* `2FA / TOTP` - "Two Factor Auth / Timed One Time Password" --> More detils on the specifics here coming soon.

The full scope of _Asymmetric Key Encryption_, Hashing, RSA, Diffie-Hellman Elliptical Curves, ratcheting and all the Cryptographic _fun_ is beyond the scope of this post. Hopefully one day I can write my love letter to crypto, but for now let's carry on by looking at each of components of `SSH.`
