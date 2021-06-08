# Filesystem / Storage Info

### tar

`tar -czvf Volume-Name.tar.gz /path/to/directory-or-file`

-   Compress Directory into `.tar.gz` extension.
-   `-c` - Create new archive.
-   `-z` - `gzip`.
-   `-v` - Create with `Volume-Name`.
-   `-f` - Specify Archive File/Device.

-----

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

-----

### ls

`ls -altr`

-   `-C` - list entries by columns.

-   `-ult` - sort  by, and show, access time.

-   `-t` - Sort by modification time, newest first.

-   `-r` - Reverse order while sorting.

-   `-l` - Use a long listing format.

-   `-d` - List directories, not their contents.

-   `-g` - Similar to `-l`, but w/o `Owner.`

-   `-R` - List subdirectories recursively.

-   `-G` - Don't print group names.

-   `-i` - Print the index number of each file (inode).

-----

### tree

`tree -aCDAh --du`

-   `-a` - Show all files.

-   `-C` - Colorization on.

-   `-D` - Last modification date.

-   `-A` - Use ANSI line graphics.

-   `-h` - Human readable file sizes.

-   `--du` - Directory sizes.

-----

### du

`du -Sh | sort -rh | head -5`

-   finds the largest directories under the current directory.

`sudo du --inodes -d 3 / | sort -n | tail`

-   Find the directory with the highest inode count using `du`.

`du -h --si |sort -rh | head -5`

-   Finds Largest Directories under the current directory for FreeNAS/FreeBSD.
