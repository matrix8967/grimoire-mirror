# Vocab - Word Bank

* `Client` - The device you're using to reach out and establish a connection with a remote host. Likely your laptop, or some kind of proxy a.k.a "Bastion Host."

* `Host` - This is the machine you're connecting *to* from your client.

* `Keypair` - This is a set of two or more cryptographic keys that are created and exchanged in order to provide  cryptographic authentication to systems. Another common use for these keypairs is _finding the least fun person at a party_ - or so I've been told.

* `Public Key` - A Public Key is one-half of our keypair, and as the name suggests it's the half that is shared with the remote Host. The Host uses it as at least one authentication mechanism to check against the Private Key.

* `Private Key` - The Private key is the half that should only live on your client machine or encrypted in a trusted secrets manager.

* `2FA / TOTP` - "Two Factor Auth / Timed One Time Password" --> More detils on the specifics here coming soon.

The full scope of _Asymmetric Key Encryption_, Hashing, RSA, Diffie-Hellman Elliptical Curves, ratcheting and all the Cryptographic _fun_ is beyond the scope of this post. Hopefully one day I can write my love letter to crypto, but for now let's carry on by looking at each of components of `SSH.`
