# MacOS

## Resources Straight from the Orchard:

-   Apple Preboot Key Combinations / Hot Keys -

    -   `https://support.apple.com/en-us/HT201255`

-   Reset SMC Chip -

    -   `https://support.apple.com/en-us/HT201295`

-   Reset PRRAM/NVRAM -

    -   `https://support.apple.com/en-us/HT204063`

-   Reinstalling MacOS from Recovery -

    -   `https://support.apple.com/en-us/HT204904`

-   Check Apple Warranty -

    -   `https://checkcoverage.apple.com/`

-   Misc. Support Site:

    -   `https://getsupport.apple.com`

* * *

## MacOS Log Locations:

-   System Log Folder
    		\* `/var/log`
-   System Log
    		\* `/var/log/system.log`
-   Mac Analytics Data
    		\* `/var/log/DiagnosticMessages`
-   System Application Logs
    		\* `/Library/Logs`
-   System Reports
    		\* `/Library/Logs/DiagnosticReports`
-   User Application Logs
    		\* `~/Library/Logs`
-   User Reports
    		\* `~/Library/Logs/DiagnosticReports`

* * *

### MacOS Wifi Strength

```sh
#!/bin/zsh

while i=1; do echo -ne 'Wifi signal strength:' $(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | grep CtlRSSI | awk {'print $2'}) '\r'; sleep 0.5; done
```
