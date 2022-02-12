# Filesystem / Storage Info

* * *

### find

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

* * *

### ls

`ls -altr`

-   `C` - list entries by columns.

-   `ult` - sort  by, and show, access time.

-   `t` - Sort by modification time, newest first.

-   `r` - Reverse order while sorting.

-   `l` - Use a long listing format.

-   `d` - List directories, not their contents.

-   `g` - Similar to `-l`, but w/o `Owner.`

-   `R` - List subdirectories recursively.

-   `G` - Don't print group names.

-   `i` - Print the index number of each file (inode).

* * *

### tree

`tree -aCDAh --du`

-   `a` - Show all files.

-   `C` - Colorization on.

-   `D` - Last modification date.

-   `A` - Use ANSI line graphics.

-   `h` - Human readable file sizes.

-   `--du` - Directory sizes.

* * *

### du

`du -Sh | sort -rh | head -5`

-   finds the largest directories under the current directory.

`sudo du --inodes -d 3 / | sort -n | tail`

-   Find the directory with the highest inode count using `du`.

`du -h --si |sort -rh | head -5`

-   Finds Largest Directories under the current directory for FreeNAS/FreeBSD.

* * *

# Rsync

`rsync -rauLvhP`

-   `r` = Recursive
-   `a` = Archive
-   `u` = Ignore Unless Newer.
-   `L` = Preserve soft links.
-   `v` = verbose
-   `h` = Human Readable
-   `P` = Progress

* * *

# TAR

`sudo /usr/bin/tar -czpvf /home/$USER/backup/Backup.tar.gz /`

-   `c` = Archive.

-   `z` =  Use GZip format to backup. GZip is fast but it generates a larger file size than other compression tools.

-   `p` =  Preserve permission so that when you restore the backup you will not encounter a permission problem.

-   `v` =  Show details during backup. Omit -v if you don't want to see verbose output.

-   `f` =  Specify where to store the tar files. Here we save the backup file to backup directory under user John's home directory and name it Backup.tar.gz.

-   `/` = The Linux root file system.

# Exclusions:

`sudo /usr/bin/tar --exclude-from=/home/$USER/tar_exclude.txt -czpvf /home/$USER/backup/Backup.tar.gz /`

## tar_exclude.txt

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

# Timestamp Backups:

`sudo /usr/bin/tar --exclude-from=/home/$USER/tar_exclude.txt -czpvf /home/$USER/backup/Backup-$(date +%F-%H-%M).tar.gz /`

# Script:

```bash,editable
#!bin/bash
tarfile=/home/$USER/backup/linux_backup-$(date +%F-%H-%M).tar.xz
sudo /usr/bin/tar --exclude-from=/home/$USER/exclude.txt -cJpvf $ /
```
