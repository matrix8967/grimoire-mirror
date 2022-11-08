# MacOS

🍎️🗒️

# Apple Networking

```sh
sudo ipconfig set en0 DHCP
```

-   Renew DHCP Lease.

```sh
sudo dscacheutil -flushcache && sudo killall -HUP mDNSResponder
```

-   Clear DNS Cache.

## Avahi Daemon

```bash
# Disable
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array-add "-NoMulticastAdvertisements"
```

```sh
# Enable (Default)
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array "/usr/sbin/mDNSResponder" "-launchd"
```

## Set Static IP Address
```sh
networksetup -setmanual "Ethernet" 192.168.2.100 255.255.255.0 192.168.2.1
```

## Wireless:

```sh
/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}'
```
-   Show current `SSID`.

```sh
defaults read /Library/Preferences/SystemConfiguration/com.apple.airport.preferences | grep LastConnected -A 7
```

-   Show Connection History.


```sh
security find-generic-password -D "AirPort network password" -a "SSID" -gw
```

-   Show SSID Passwords.


```sh
networksetup -setairportpower en0 on
```

-   Turn on wifi Adapter.

## Measure Wireless Strength from CLI:

```bash
#!/bin/zsh
while i=1; do echo -ne 'Wifi signal strength:' $(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | grep CtlRSSI | awk {'print $2'}) '\r'; sleep 0.5; done
```

## Forget SSID

```bash
#!/bin/bash

SSID=$(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | grep SSID | grep -v BSSID | awk '{print $2,$3,$4,$5}')

networksetup -removepreferredwirelessnetwork en0 $SSID
networksetup -setnetworkserviceenabled Wi-Fi off
networksetup -setnetworkserviceenabled Wi-Fi on
unset SSID

exit 0
```

## Create a symbolic link to the airport command for easy access:
```sh
sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/local/bin/airport
```
## Run a wireless scan with Symbolic Link:
```sh
airport -s
```

-----

## Firewall:
```sh
# Show Status
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate

# Enable
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate on

# Disable (Default)
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --setglobalstate off
```

## Add Application to Firewall
```sh
sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /path/to/file
```

-----

# Filevault

```sh
sudo fdesetup status
```

-   Filevault Status.

```sh
sudo fdesetup enable
```

-   Filevault Enable.

-----

# Time Machine:

## Prevent Time Machine from Prompting to Use New Drives:

```sh
sudo defaults write /Library/Preferences/com.apple.TimeMachine DoNotOfferNewDisksForBackup -bool true
```

## Show Time Machine Logs:

```sh
#!/bin/sh

filter='processImagePath contains "backupd" and subsystem beginswith "com.apple.TimeMachine"'

# show the last 12 hours
start="$(date -j -v-12H +'%Y-%m-%d %H:%M:%S')"

echo ""
echo "[History (from $start)]"
echo ""

log show --style syslog --info --start "$start" --predicate "$filter"

echo ""
echo "[Following]"
echo ""

log stream --style syslog --info --predicate "$filter"
```

## Time Machine Stats:

```sh
# List all backups
tmutil listbackups

# Show differences
tmutil calculatedrift /path/to/backup/folder/plus/machine/name/folder
```

## Verify Backup

```sh
sudo tmutil verifychecksums /path/to/backup
```

-----

# Disk Images

## Create Disk Image From Folder Contents
```sh
hdiutil create -volname "Volume Name" -srcfolder /path/to/folder -ov diskimage.dmg
```

If you'd like to encrypt the disk image:
```sh
hdiutil create -encryption -stdinpass -volname "Volume Name" -srcfolder /path/to/folder -ov encrypted.dmg
```

By default, you'll be prompted for a password. You can automate that by piping
in a password:
```sh
echo -n YourPassword | hdiutil create -encryption -stdinpass -volname "Volume Name" -srcfolder /path/to/folder -ov encrypted.dmg
```

## Burn Disk Images to DVD
This command applies to .iso, .img and .dmg images.
```sh
hdiutil burn /path/to/image_file
```

## Disable Disk Image Verification
```sh
defaults write com.apple.frameworks.diskimages skip-verify -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-locked -bool true && \
defaults write com.apple.frameworks.diskimages skip-verify-remote -bool true
```

## Make Volume OS X Bootable
```sh
bless --folder "/path/to/mounted/volume/System/Library/CoreServices" --bootinfo --bootefi
```

## Mount Disk Image
```sh
hdiutil attach /path/to/diskimage.dmg
```

## Unmount Disk Image
```sh
hdiutil detach /dev/disk2s1
```

## Write Disk Image to Volume
Like the Disk Utility "Restore" function.
```sh
sudo asr -restore -noverify -source /path/to/diskimage.dmg -target /Volumes/VolumeToRestoreTo
```

-----

# Hardware Misc:

## List All Hardware Ports
```sh
networksetup -listallhardwareports
```

## Remaining Battery Percentage
```sh
pmset -g batt | egrep "([0-9]+\%).*" -o --colour=auto | cut -f1 -d';'
```

## Remaining Battery Time
```sh
pmset -g batt | egrep "([0-9]+\%).*" -o --colour=auto | cut -f3 -d';'
```

## Show Connected Device's UDID
```sh
system_profiler SPUSBDataType | sed -n -e '/iPad/,/Serial/p' -e '/iPhone/,/Serial/p'
```

## Show Current Screen Resolution
```sh
system_profiler SPDisplaysDataType | grep Resolution
```

## Show CPU Brand String
```sh
sysctl -n machdep.cpu.brand_string
```

## Prevent System Sleep
Prevent sleep for 1 hour:
```sh
caffeinate -u -t 3600
```

## Show All Power Management Settings
```sh
sudo pmset -g
```

## Put Display to Sleep after 15 Minutes of Inactivity
```sh
sudo pmset displaysleep 15
```

## Put Computer to Sleep after 30 Minutes of Inactivity
```sh
sudo pmset sleep 30
```

## Check System Sleep Idle Time
```sh
sudo systemsetup -getcomputersleep
```

## Set System Sleep Idle Time to 60 Minutes
```sh
sudo systemsetup -setcomputersleep 60
```

## Turn Off System Sleep Completely
```sh
sudo systemsetup -setcomputersleep Never
```

## Automatic Restart on System Freeze
```sh
sudo systemsetup -setrestartfreeze on
```

-----

# Finder:

## Show External Media

```sh
# Enable
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true && \
killall Finder

# Disable (Default)
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool false && \
killall Finder
```

## Show Internal Media

```sh
# Enable
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true && \
killall Finder

# Disable (Default)
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool false && \
killall Finder
```

## Show Removable Media

```sh
# Enable
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true && \
killall Finder

# Disable (Default)
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool false && \
killall Finder
```

## Show Network Volumes

```sh
# Enable
defaults write com.apple.finder ShowMountedServersOnDesktop -bool true && \
killall Finder

# Disable (Default)
defaults write com.apple.finder ShowMountedServersOnDesktop -bool false && \
killall Finder
```

## Increase Number of Recent Places
```sh
defaults write -g NSNavRecentPlacesLimit -int 10 && \
killall Finder
```

## Show All File Extensions
```sh
defaults write -g AppleShowAllExtensions -bool true
```

## Show Hidden Files
```sh
# Show All
defaults write com.apple.finder AppleShowAllFiles true

# Restore Default File Visibility
defaults write com.apple.finder AppleShowAllFiles false
```

## Show Full Path in Finder Title
```sh
defaults write com.apple.finder _FXShowPosixPathInTitle -bool true
```

## Toggle Folder Visibility in Finder
By default, the `~/Library` folder is hidden. You can easily show it again. The
same method works with all other folders.
```sh
# Hidden (Default)
chflags hidden ~/Library

# Visible
chflags nohidden ~/Library
```
## Expand Save Panel by Default
```sh
defaults write -g NSNavPanelExpandedStateForSaveMode -bool true && \
defaults write -g NSNavPanelExpandedStateForSaveMode2 -bool true
```

## Desktop Icon Visibility
```sh
# Hide Icons
defaults write com.apple.finder CreateDesktop -bool false && \
killall Finder

# Show Icons (Default)
defaults write com.apple.finder CreateDesktop -bool true && \
killall Finder
```

## Path Bar
```sh
# Show
defaults write com.apple.finder ShowPathbar -bool true

# Hide (Default)
defaults write com.apple.finder ShowPathbar -bool false
```

## Scrollbar Visibility
Possible values: `WhenScrolling`, `Automatic` and `Always`.
```sh
defaults write -g AppleShowScrollBars -string "Always"
```

## Status Bar
```sh
# Show
defaults write com.apple.finder ShowStatusBar -bool true

# Hide (Default)
defaults write com.apple.finder ShowStatusBar -bool false
```

## Save to Disk by Default
Sets default save target to be a local disk, not iCloud.
```sh
defaults write -g NSDocumentSaveNewDocumentsToCloud -bool false
```

## Set Current Folder as Default Search Scope
```sh
defaults write com.apple.finder FXDefaultSearchScope -string "SCcf"
```

## Set Default Finder Location to Home Folder
```sh
defaults write com.apple.finder NewWindowTarget -string "PfLo" && \
defaults write com.apple.finder NewWindowTargetPath -string "file://${HOME}"
```

## Recursively Delete .DS_Store Files
```sh
find . -type f -name '.DS_Store' -ls -delete
```

-----

# Kernel Extensions

```sh
sudo kextstat -l
```

-   List Kernel Extensions

```sh
sudo kextunload -b com.apple.driver.ExampleSomething
```

-   Unload Kernel Extensions

-----

# Updates

```sh
sudo softwareupdate -ia`

-   Install all available updates.

```sh
defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1
```
-   Change the Update Checking Interval.

```sh
sudo softwareupdate --list
```

-   Show available updates.

-----

# Audio:

```sh
sudo osascript -e "set Volume 0"
```

-   Mute Audio.


## Chime on Charge:

```sh
# Enable (Default)
defaults write com.apple.PowerChime ChimeOnNoHardware -bool false && \
open /System/Library/CoreServices/PowerChime.app

# Disable
defaults write com.apple.PowerChime ChimeOnNoHardware -bool true && \
killall PowerChime
```

## Startup Chime:

```sh
# Enable
sudo nvram StartupMute=%00

# Disable (Default)
sudo nvram StartupMute=%01

# Alt:
sudo nvram SystemAudioVolume=" "
```

## Convert Audio File to iPhone Ringtone
```sh
afconvert input.mp3 ringtone.m4r -f m4af
```

## Create Audiobook From Text
Uses "Alex" voice, a plain UTF-8 encoded text file for input and AAC output.
```sh
say -v Alex -f file.txt -o "output.m4a"
```

## Play Audio File
You can play all audio formats that are natively supported by QuickTime.
```sh
afplay -q 1 filename.mp3
```

## Speak Text with System Default Voice
```sh
say 'All your base are belong to us!'
```

-----

# Apps:

## List All Apps Downloaded from App Store

```sh
# Via find
find /Applications -path '*Contents/_MASReceipt/receipt' -maxdepth 4 -print |\sed 's#.app/Contents/_MASReceipt/receipt#.app#g; s#/Applications/##'

# Via Spotlight
mdfind kMDItemAppStoreHasReceipt=1
```

-----

# SSH:

-----

# Apple Remote Desktop:

## Activate And Deactivate the ARD Agent and Helper
```sh
# Activate And Restart the ARD Agent and Helper
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -restart -agent -console

# Deactivate and Stop the Remote Management Service
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -stop
```

## Remote Desktop Sharing
```sh
# Allow Access for All Users and Give All Users Full Access
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -configure -allowAccessFor -allUsers -privs -all

# Disable ARD Agent and Remove Access Privileges for All Users (Default)
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -deactivate -configure -access -off
```

## Remove Apple Remote Desktop Settings
```sh
sudo rm -rf /var/db/RemoteManagement ; \
sudo defaults delete /Library/Preferences/com.apple.RemoteDesktop.plist ; \
defaults delete ~/Library/Preferences/com.apple.RemoteDesktop.plist ; \
sudo rm -r /Library/Application\ Support/Apple/Remote\ Desktop/ ; \
rm -r ~/Library/Application\ Support/Remote\ Desktop/ ; \
rm -r ~/Library/Containers/com.apple.RemoteDesktop
```

-----

# Fonts:

## Clear Font Cache for Current User

```sh
atsutil databases -removeUser && \
atsutil server -shutdown && \
atsutil server -ping
```

## Get SF Mono Fonts

```sh
cp -v /Applications/Xcode-beta.app/Contents/SharedFrameworks/DVTKit.framework/Versions/A/Resources/Fonts/SFMono-* ~/Library/Fonts
```

-----

# Logs & Reporting:

## System Software Version

```sh
sw_vers -productVersion
```
```sh
system_profiler SPSoftwareDataType
```
```sh
defaults read loginwindow SystemVersionStampAsString
```

```sh
sudo sysdiagnose -f ~/Desktop/
```

-   Run performance / diagnostic and place results on the Desktop.

```sh
mdutil -E /path/to/volume
```

-   Erase & Rebuild `Spotlight` Search.

```sh
/usr/bin/profiles list --type configuration --output stdout-xml
```

-   Dump Profiles to XML.

-----

# Links:

## MacOS Deployment Overview:

-   [Deployment Overview.](https://www.apple.com/business/docs/site/Mac_Deployment_Overview.pdf)
-   [AppleSeed IT Guide.](https://www.apple.com/business/docs/resources/AppleSeed_for_IT_Guide.pdf)
-   [MacOS SSO.](https://support.apple.com/guide/deployment-reference-macos/single-sign-on-extension-apdac83c038d/web)
-   [Identity Mgmt.](https://support.apple.com/guide/deployment-reference-macos/intro-to-identity-management-apd28d472300/web)

## MacOS Networking Articles:

-   [WiFi Coverage.](https://support.apple.com/guide/deployment-reference-macos/getting-proper-wi-fi-coverage-iorb54f75587/web)
-   [fkn mDNS.](https://support.apple.com/guide/deployment-reference-macos/intro-to-bonjour-apd0401947ff/web)
-   [AD Integration.](https://support.apple.com/guide/deployment-reference-macos/integrating-macos-with-active-directory-iorbeda89d1d/web)
-   [Private Relay.](https://support.apple.com/en-us/HT212614)

-----

## MacOS Support Pages:

Useful for users.

-   MacOS / Device Network Ports:

-   <https://support.apple.com/en-us/HT210060>

-   Apple Preboot Key Combinations / Hot Keys:

-   <https://support.apple.com/en-us/HT201255>

-   Reset SMC Chip:

-   <https://support.apple.com/en-us/HT201295>

-   Reset PRRAM/NVRAM:

-   <https://support.apple.com/en-us/HT204063>

-   Reinstalling MacOS from Recovery:

-   <https://support.apple.com/en-us/HT204904>

-   Check Apple Warranty:

-   <https://checkcoverage.apple.com/>

-   Misc. Support Site:

-   <https://getsupport.apple.com>

-----

# MacOS VMs:

> TO-DO.

![MacOS VM](../Images/MacOSVM.png)

# MacOS Automated Setup:

> TO-DO.

<script id="asciicast-BIkZBwZxJ3jA2owDqMpf7ScBF" src="https://asciinema.org/a/BIkZBwZxJ3jA2owDqMpf7ScBF.js" data-autoplay="true" data-loop="true" async></script>
