# SSH_Notes

### Testing & Restarting the SSH Daemon Service:

`sudo sshd -t`

-   Test the `sshd_config` file for errors before reloading / restarting the service.

`/usr/sbin/sshd -D -p 2222`

-   Create a new `ssh` instance in the foreground on a separate port as a failsafe shell. (like when editing `/etc/ssh/sshd_config`)

* * *

## Create RAW Disk Image over SSH:

`ssh $HOST 'sudo -S dd if=/dev/$STORAGE_BLKID ' | dd of=filename.img`

* * *

### Connect to remote host on Port 22 through a Jump Host:

`ssh -J $JUMP-USER@$JUMP-HOST -p 22 $REMOTE-USER@$REMOTE-HOST`

* * *

### Tunnel RDP Connections over SSH Tunnel from a Control Node:

```bash
#!/usr/bin/env bash
set -euo pipefail

RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m' # No Color

scriptname="$(basename $0)"

if [ $# -lt 3 ]
 then
    echo "Usage: $scriptname start | stop  RDP_NODE_IP  SSH_NODE_IP SSH_LOCAL_PORT"
    exit
fi

case "$1" in

start)

  echo "Starting tunnel to $3"
  ssh -M -S ~/.ssh/$scriptname.${4:-3389}.control -fnNT -L ${4:-3389}:$2:3389 $3
  ssh -S ~/.ssh/$scriptname.${4:-3389}.control -O check $3
  ;;

stop)
  echo "Stopping tunnel to $3"
  ssh -S ~/.ssh/$scriptname.${4:-3389}.control -O exit $3

 ;;

*)
  echo "Did not understand your argument, please use start|stop"
  ;;

esac
```


`~/.ssh/rdp-tunnel.sh start $REMOTE_CLIENT $CONTROL_NODE_IP $LOCAL_PORT`

-   Pre Command. ^^

`~/.ssh/rdp-tunnel.sh stop $REMOTE_CLIENT $CONTROL_NODE_IP $LOCAL_PORT`

-   Post Command. ^^

`localhost:LOCAL_PORT`

-   Address for RDP Tunnel on the SSH Control Node. ^^

* * *

## RSync:

```bash
rsync -razuvhLP --exclude 'directory01' --exclude '*.ssh' --remove-source-files --info=progress2 -e "ssh -i /home/$USER/.ssh/keyfile" /home/example_directory $REMOTE_USER@$REMOTE_HOST:/home/$USER/rsync_destination/ > /home/$USER/rsync_Output.txt
```

An example _one liner_ using RSync to back up a directory to a remote host, while:

* excludes certain directories.
* Shows Progress Info.
* Logs `stdout` & `stder` to a logfile.
* Removes the Source Files upon successful completion of transfer.
  * (Validation Methods can be customized: Filesize, Hashsums, etc.)
* Specifies a non-default `keyfile` for Authentication.
* Uses the following RSync Flags:
  * [r]ecursively
  * [a]rchive
  * Resolve Soft[l]inks
  * Ignore Duplicates [u]nless newer.
  * Display [h]uman-readable [P]rogress.
