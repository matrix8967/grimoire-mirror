# Git Config

```
[user]
	email = $EMAIL
	name = $USERNAME
	signingkey = $FINGERPRINT_OF_GPG_SIGNING_KEY

[commit]
	gpgsign = true

[pull]
	rebase = false

[filter "lfs"]
	process = git-lfs filter-process
	required = true
	clean = git-lfs clean -- %f
	smudge = git-lfs smudge -- %f
```

* Default for `~/.gitconfig`.
