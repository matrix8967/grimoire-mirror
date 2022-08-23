# minicom Config File

Config file to setup defaults for working with Ubiquiti [Edgerouter](https://help.ui.com/hc/en-us/articles/205202630-EdgeRouter-How-to-Connect-to-Serial-Console)/[Edgeswitch](https://help.ui.com/hc/en-us/articles/360002434334) hardware using a [DB-9/Rollover/Console cable.](src/Images/DB9.jpg)

```
# Machine-generated file - use "minicom -s" to change parameters.
pu port             /dev/ttyUSB0
pu baudrate         115200
pu bits             8
pu parity           N
pu stopbits         1
pu rtscts           No
```

Location: `/etc/minicom/minirc.edgeos.dfl`

