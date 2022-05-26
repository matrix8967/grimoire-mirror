# Android

# adb

`adb shell pm list packages | cut -d ":" -f 2`

-   Lists all installed apps on device.
-   Useful to save this for future reference.

`adb shell pm path $PACKAGE_NAME`

-   Lists the path of `$PACKAGE_NAME`'s installation `.APK` file.

`adb uninstall --user 0 $PACKAGE_NAME`

-   Uninstalls `$PACKAGE_NAME` for user.
-   Useful for debloating.
-   `adb shell pm list users` to get user ID. Default 0.

* * *

### APK_Pull.sh

Script to use `ADB`'s built in shell and `packagemanager` (`pm`) to pull `.APK` installers from all the currently installed packages on a system. Depending on the AndroidOS version - this might need some testing & tweaking.

```bash,editable
#!/usr/bin/env bash

for i in $(sudo adb shell pm list packages | awk -F':' '{print $2}'); do
  sudo adb pull "$(sudo adb shell pm path $i | awk -F':' '{print $2}')";
  mv base.apk $i.apk &> /dev/null
done
```

* * *

### Full raw disk image over ADB:

Requires `root`.

```bash
adb forward tcp:5555 tcp:5555
adb shell
su
nc -l -p 5555 dd if=/dev/block/mmcblk0
```

-   Setup ADB networking and forward ports.
-   Start `ADB` shell on Device.
-   Elevate to `root`.
-   Start `netcat` listener on `ADB` port.
-   Sets the execution program as `dd` & sets `inputfile` as the Device's Block Storage.

In a new terminal:

```bash
nc 127.0.0.1 5555 | pv -i 0.5 > Raw_Image_File_Name.raw
```
* * *

# Termux

> TO DO

* * *
# scrcpy

`scrcpy -SwK -m 1920`

-   `S` - Turn off device screen upon connection.
-   `w` - Stay Awake -- disables screen timeout while connected to `scrcpy`.
-   `k` - Simulate physical keyboard connection.
-   `m` - Max Size -- limits the framebuffer width & height to value.

## Full `scrcpy` reference:

```
--always-on-top               -- Make scrcpy window always on top (above other windows)
--bit-rate                -b  -- Encode the video at the given bit-rate
--codec-options               -- Set a list of comma-separated key:type=value options for the device encoder
--crop                        -- [width:height:x:y] Crop the device screen on the server
--disable-screensaver         -- Disable screensaver while scrcpy is running
--display                     -- Specify the display id to mirror
--display-buffer              -- Add a buffering delay (in milliseconds) before displaying
--encoder                     -- Use a specific MediaCodec encoder (must be a H.264 encoder)
--force-adb-forward           -- Do not attempt to use "adb reverse" to connect to the device
--forward-all-clicks          -- Forward clicks to device
--fullscreen              -f  -- Start in fullscreen
--help                    -h  -- Print the help
--hid-keyboard            -K  -- Simulate a physical keyboard by using HID over AOAv2
--hid-mouse               -M  -- Simulate a physical mouse by using HID over AOAv2
--legacy-paste                -- Inject computer clipboard text as a sequence of key events on Ctrl+v
--lock-video-orientation      -- Lock video orientation
--max-fps                     -- Limit the frame rate of screen capture
--max-size                -m  -- Limit both the width and height of the video to value
--no-cleanup                  -- Disable device cleanup actions on exit
--no-clipboard-autosync       -- Disable automatic clipboard synchronization
--no-control              -n  -- Disable device control (mirror the device in read only)
--no-display              -N  -- Do not display device (during screen recording or when V4L2 sink is enabled)
--no-downsize-on-error        -- Disable lowering definition on MediaCodec error
--no-key-repeat               -- Do not forward repeated key events when a key is held down
--no-mipmaps                  -- Disable the generation of mipmaps
--otg                         -- Run in OTG mode (simulating physical keyboard and mouse)
--port                    -p  -- [port[:port]] Set the TCP port (range) used by the client to listen
--power-off-on-close          -- Turn the device screen off when closing scrcpy
--prefer-text                 -- Inject alpha characters and space as text events instead of key events
--print-fps                   -- Start FPS counter, to print frame logs to the console
--push-target                 -- Set the target directory for pushing files to the device by drag and drop
--raw-key-events              -- Inject key events for all input keys, and ignore text events
--record                  -r  -- Record screen to file
--record-format               -- Force recording format
--render-driver               -- Request SDL to use the given render driver
--rotation                    -- Set the initial display rotation
--select-tcpip            -e  -- Use TCP/IP device
--select-usb              -d  -- Use USB device
--serial                  -s  -- The device serial number (mandatory for multiple devices only)
--shortcut-mod                -- [key1,key2+key3,...] Specify the modifiers to use for scrcpy shortcuts
--show-touches            -t  -- Show physical touches
--stay-awake              -w  -- Keep the device on while scrcpy is running, when the device is plugged in
--tcpip                       -- (optional [ip:port]) Configure and connect the device over TCP/IP
--tunnel-host                 -- Set the IP address of the adb tunnel to reach the scrcpy server
--tunnel-port                 -- Set the TCP port of the adb tunnel to reach the scrcpy server
--turn-screen-off         -S  -- Turn the device screen off immediately
--v4l2-buffer                 -- Add a buffering delay (in milliseconds) before pushing frames
--v4l2-sink                   -- [/dev/videoN] Output to v4l2loopback device
--verbosity               -V  -- Set the log level
--version                 -v  -- Print the version of scrcpy
--window-borderless           -- Disable window decorations (display borderless window)
--window-height               -- Set the initial window height
--window-title                -- Set a custom window title
--window-width                -- Set the initial window width
--window-x                    -- Set the initial window horizontal position
--window-y                    -- Set the initial window vertical position
```
