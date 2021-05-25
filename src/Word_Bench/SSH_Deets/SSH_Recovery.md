# Recovery/Break Glass of remote hosts.

  * `/usr/sbin/sshd -D -p 2222` --> This will spawn a new SSH Daemon Process on the specified port to act as a recovery in case a remote shell is terminated, so long as the parent process stays alive.

* Absolute Break Glass (modifying broken `sshd.conf`, etc.)
    + Bring down `EC2` Instance,
    + Disconnect the `rootfs`
    + Mount the `rootfs` to another `EC2`.
    + Edit what you need. Follow steps in reverse.

* 05-25-21 update -- LOL Amazon *FINALLY* added a recovery/Serial option to `EC2`
* So fucking glad _papa beezers_ learned to catch up with what - the 1970's?
* I mean FFS - they're _the last_ VPC I've heard of to not offer...basic recovery tools? lol wtf - people fkn pay for this shit dude.

-----

First pass at this won't be great - but it'll be better than what we have now:

It'll be done _somewhat_ manually - I can't think of any _major_ changes on the `SSH` versions of even our oldest infra. But it's worth a peek - specifically `Ingest` which I'd prefer to do near last since it's the oldest and most risky for `SSH` operations.

I'm hoping to start moving more and more of this "legacy" infra into Ansible - and (with peer approval) I'd like to see it start here.

Either way - before we make any changes we should:

1.) Backup the `~/.ssh/`, `/etc/ssh/`, and `/etc/pam.d` directories on each host.

2.) Make our change(s).

3.) `sudo sshd -t` (tests the `sshd.conf` for issues.

4.) run `/usr/sbin/sshd -D -p 2222` to establish a fail-safe SSH Session.

If all that fails:

* Shutdown EC2 Instance
* Disconnect `rootfs` / `root EBS`
* Attach to a new EC2 Instance (can be a `t2micro`.)
* Create a mount new point for busted EC2 machine's `rootfs`
	* `sudo mkdir /mnt/uh_oh`
* Mount the busted EC2's `rootfs` to the mountpoint:
	* `sudo mount -t ext4 /dev/vdb1 /mnt/uh_oh`
	* (Assuming default of an `ext4` FS. Use `lsblk` and `df -h` and/or `fdisk -l` for more info.)
* Fix wut broke. 👍️🔧️
* Shutdown the temp EC2 instance.
* Reattach previously fkd up `rootfs`.
* 📿️🙏️👼️👹️pull out all the stops while appealing to divinity.
* `exit=0` --> Enjoy a restored SSH Connection
* `exit=1` --> `Generate Resume.`
