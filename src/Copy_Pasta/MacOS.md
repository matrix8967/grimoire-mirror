# MacOS Wifi Strenth

`while i=1; do echo -ne 'Wifi signal strength:' $(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | grep CtlRSSI | awk {'print $2'}) '\r'; sleep 0.5; done`

`(from: https://www.commandlinefu.com/commands/view/11826/continuously-show-wifi-signal-strength-on-a-mac)`
