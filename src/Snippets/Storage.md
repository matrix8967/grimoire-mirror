# Finding Things

* * *

## find

`find . -type d | cut -d/ -f 2 | uniq -c`
-   Find the number of directories under the current directory

`find . -type d | sed -e "s/[^-][^\/]*\// |/g" -e "s/|\([^ ]\)/|-\1/"`
-   This will tree the current directory.

`find -type f -exec du -Sh {} + | sort -rh | head -n 5`
-   This will find the largest files in the current subdir.

`find /home/$USER/temp/* -mtime +10 -type f -delete`
-   find and delete files or directories by replacing `f` with `d`

`sudo find . -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n`
-   Finds the directory with the highest number of inodes under the current directory.

## tree

`tree -aCDAh --du`

-   `a` - Show all files.
-   `C` - Colorization on.
-   `D` - Last modification date.
-   `A` - Use ANSI line graphics.
-   `h` - Human readable file sizes.
-   `--du` - Directory sizes.

* * *

## du

`du -Sh | sort -rh | head -5`
-   finds the largest directories under the current directory.

`sudo du --inodes -d 3 / | sort -n | tail`
-   Find the directory with the highest inode count using `du`.

`du -h --si |sort -rh | head -5`
-   Finds Largest Directories under the current directory for FreeNAS/FreeBSD.

* * *

# Doing Things

### Rsync

`rsync -rauLvhP`

-   `r` = Recursive
-   `a` = Archive
-   `u` = Ignore Unless Newer.
-   `L` = Preserve soft links.
-   `v` = verbose
-   `h` = Human Readable
-   `P` = Progress

* * *

## TAR

`sudo /usr/bin/tar -czpvf /home/$USER/backup/Backup.tar.gz /`

-   `c` = Archive.
-   `z` =  Use GZip format to backup. GZip is fast but it generates a larger file size than other compression tools.
-   `p` =  Preserve permission so that when you restore the backup you will not encounter a permission problem.
-   `v` =  Show details during backup. Omit -v if you don't want to see verbose output.
-   `f` =  Specify where to store the tar files. Here we save the backup file to backup directory under user John's home directory and name it Backup.tar.gz.
-   `/` = The Linux root file system.

### Exclusions:

`sudo /usr/bin/tar --exclude-from=/home/$USER/.tar_exclude.txt -czpvf /home/$USER/backup/Backup.tar.gz /`

### tar_exclude.txt

```
            /home/$USER/backup/*
            /tmp/*
            /proc/*
            /dev/*
            /sys/*
            /run/*
            /var/tmp/*
            /var/run/*
            /var/lock/*
            /usr/portage/*
            /usr/src/*
```

#### Timestamp Backups:

`sudo /usr/bin/tar --exclude-from=/home/$USER/.tar_exclude.txt -czpvf /home/$USER/backup/Backup-$(date +%F-%H-%M).tar.gz /`

### Script:

```bash
#!bin/sh
tarfile=/home/$USER/backup/linux_backup-$(date +%F-%H-%M).tar.xz
sudo /usr/bin/tar --exclude-from=/home/$USER/exclude.txt -cJpvf $ /
```
* * *

## Erasing files & Devices:

### `dd`

`dd if=/dev/zero of=/dev/sdX bs=1M &`

-   `if` = Input File.
-   `of` = Output File.
-   `bs` = R/W size in bytes. (Default = 512 bytes.)

### shred

`shred --iterations=35 --verbose --zero --remove {FILE}`

-   `iterations` = number of times to pass over the drive.
-   `zero` = Overwrite with zeroes
-   `remove` = Overwrite and remove.

## Recovery

### Foremost

`sudo foremost -a -T -t jpg,bmp,gif,png,avi,mpg -i /dev/sdc`

-   `-a` Enables all write headers -- pushes corrupt files (Usually Windows/NTFS).
-   `-d` Indirect block detection (Used for *nix systems.)
-   `-T` Time Stamps the dirs (Prevents overwriting subsequent runs of Foremost.)
-   `-t` Specify the filetype(s) for recovery.
-   `-i` Input (The path to the target _device_. i.e. `/dev/sdX`)
-   `-o` Output (Defaults to Current Dir if unspecified.)
