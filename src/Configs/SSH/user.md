# User SSH Config

* * *

## User SSH Config:

Instead of defining _functions_ or _variables_ in your `$PATH` - defining a `config` file for `ssh` commonly used connections is recommended. An example of an entry is shown below.

On _most_ `*nix` based systems - the default `ssh-config` file for a user is stored in `~/.ssh/config`.

When in doubt, consult your system's global `ssh` config file(s).

Example `config` with some common configuration options:

```
Host $CONNECTION-NAME
  Hostname $REMOTE-HOST
  Port $REMOTE-SSH-PORT
  User $REMOTE-USER
  ProxyJump $JUMP-HOST
  ForwardX11 yes
  Ciphers blowfish-cbc,arcfour
  HostkeyAlgorithms +ssh-rsa
  PubkeyAcceptedAlgorithms +ssh-rsa
```

* * *
