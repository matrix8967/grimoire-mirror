# Rsync

`rsync -rauLvhP`

-   `r` = Recursive
-   `a` = Archive
-   `z` = Compressed (zipped)
-   `u` = Ignore Unless Newer.
-   `L` = Preserve soft links.
-   `v` = verbose
-   `h` = Human Readable
-   `P` = Progress

-----

# TAR

`sudo /usr/bin/tar -czpvf /home/$USER/backup/Backup.tar.gz /`

    `-c`: Archive.

    `-z`: Use GZip format to backup. GZip is fast but it generates a larger file size than other compression tools.

    `-p`: Preserve permission so that when you restore the backup you will not encounter a permission problem.

    `-v`: Show details during backup. Omit -v if you don't want to see verbose output.

    `-f`: Specify where to store the tar files. Here we save the backup file to backup directory under user John's home directory and name it Backup.tar.gz.

    `/`: The Linux root file system.

# Exclusions:

`sudo /usr/bin/tar --exclude-from=/home/$USER/tar_exclude.txt -czpvf /home/$USER/backup/Backup.tar.gz /`

## tar_exclude.txt

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

# Timestamp Backups:

`sudo /usr/bin/tar --exclude-from=/home/$USER/tar_exclude.txt -czpvf /home/$USER/backup/Backup-$(date +%F-%H-%M).tar.gz /`

# Script:

```bash
#!bin/sh
_tarfile=/home/$USER/backup/linux_backup-$(date +%F-%H-%M).tar.xz
sudo /usr/bin/tar --exclude-from=/home/$USER/exclude.txt -cJpvf $ /
```
