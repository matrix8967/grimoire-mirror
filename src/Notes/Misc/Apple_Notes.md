# Apple_Notes

🍎️🗒️

## Apple Networking

-   <https://kean.blog/pulse/home>
    -   <https://github.com/kean/Pulse>

```bash
# Disable
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array-add "-NoMulticastAdvertisements"

# Enable (Default)
sudo defaults write /System/Library/LaunchDaemons/com.apple.mDNSResponder.plist ProgramArguments -array "/usr/sbin/mDNSResponder" "-launchd"
```

`sudo ipconfig set en0 DHCP`

-   Renew DHCP Lease.

`sudo dscacheutil -flushcache && sudo killall -HUP mDNSResponder`

-   Clear DNS Cache.


`/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | awk '/ SSID/ {print substr($0, index($0, $2))}'`

-   Show current `SSID`.

`defaults read /Library/Preferences/SystemConfiguration/com.apple.airport.preferences | grep LastConnected -A 7`

-   Show Connection History.

`security find-generic-password -D "AirPort network password" -a "SSID" -gw`

-   Show SSID Passwords.

`networksetup -setairportpower en0 on`

-   Turn on wifi Adapter.

## Filevault

`sudo fdesetup status`

-   Filevault Status.

`sudo fdesetup enable`

-   Filevault Enable.

`sudo sysdiagnose -f ~/Desktop/`

-   Run performance / diagnostic and place results on the Desktop.

## Bootable USB Installer:

```bash
    # macOS 11 (Big Sur)
    sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction --downloadassets

    # macOS 10.15 (Catalina)
    sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction --downloadassets

    # macOS 10.14 (Mojave)
    sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction --downloadassets

    # macOS 10.13 (High Sierra)
    sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ High\ Sierra.app

    # macOS 10.12 (Sierra)
    sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ Sierra.app

    # OS X 10.11 (El Capitan)
    sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app

    # OS X 10.10 (Yosemite)
    sudo /Applications/Install\ OS\ X\ Yosemite.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ OS\ X\ Yosemite.app
```

## Kernel Extensions

`sudo kextstat -l`

-   List Kernel Extensions

`sudo kextunload -b com.apple.driver.ExampleBundle`

-   Unload Kernel Extensions

## Updates

`sudo softwareupdate -ia`

-   Install all available updates.

`defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 1`

-   Change the Update Checking Interval.

`sudo softwareupdate --list`

-   Show available updates.

`mdutil -E /path/to/volume`

-   Erase & Rebuild `Spotlight` Search.# Apple_Notes
