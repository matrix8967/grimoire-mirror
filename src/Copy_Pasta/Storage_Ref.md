# Filesystem Info

`tar -czvf name-of-archive.tar.gz /path/to/directory-or-file`

	- Compress Directory into `.tar.gz` extension.

`find . -type d | cut -d/ -f 2 | uniq -c`

	* Find the number of directories under the current directory

`find . -type d | sed -e "s/[^-][^\/]*\// |/g" -e "s/|\([^ ]\)/|-\1/" `

	* This will tree the current directory.

`find -type f -exec du -Sh {} + | sort -rh | head -n 5 `

	* This will find the largest files in the current subdir.

`du -Sh | sort -rh | head -5 `

	* finds the largest directories under the current directory.

`find /home/$USER/temp/* -mtime +10 -type f -delete`

	* find and delete files or directories by replacing `f` with `d`

`sudo find . -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n`

	* Finds the directory with the highest number of inodes under the current directory.

`sudo du --inodes -d 3 / | sort -n | tail`

	* Find the directory with the highest inode count using `du`.

`du -h --si |sort -rh | head -5`

	* Finds Largest Directories under the current directory for FreeNAS/FreeBSD.
