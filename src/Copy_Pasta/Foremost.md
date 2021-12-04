# Foremost

* * *

### Foremost

`sudo foremost -a -T -t jpg,bmp,gif,png,avi,mpg -i /dev/sdc`

-   `-a` Enables all write headers -- pushes corrupt files (Usually Windows/NTFS).

-   `-d` Indirect block detection (Used for *nix systems.)

-   `-T` Time Stamps the dirs (Prevents overwriting subsequent runs of Foremost.)

-   `-t` Specify the filetype(s) for recovery.

-   `-i` Input (The path to the target _device_. i.e. `/dev/sdX`)

-   `-o` Output (Defaults to Current Dir if unspecified.)
