# Setup

## OOBE

`OOBE` is the industry term for Windows' Setup Proceedures - it's an Acronym for `Out Of Box Experience.`

During Setup - Microsoft will be _admant_ that you're _required_ to setup a Microsoft Account in order to login to your PC. While this is *not true* - it gets harder to sidestep this part of Setup with each new Windows Version.

As of this writing - this is the recommended method to setup a stand-alone, offline, local user for Windows 10 / Windows 11:

* Get to `Sign In With Microsoft Account` stage of Setup.
* Press Shift + F10 to launch terminal.
* Type: `ncpa.cpl`
* Right Click & Disable all Network Device Adapter(s).
* Go back to OOBE, retry User Setup.
* After setup is complete you can re-enable your Network Device Adapters.

## TODO:

* `OOBE` Screenshots.