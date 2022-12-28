# Apple

## Apple NetSec:

* https://proton.me/blog/apple-ad-company
* https://github.com/FSecureLABS/macOSTriageCollectionScript
* https://github.com/FSecureLABS/Jamf-Attack-Toolkit
* https://labs.f-secure.com/blog/jamfing-for-joy-attacking-macos-in-enterprise/
* https://github.com/drduh/macOS-Security-and-Privacy-Guide
* https://ahmedmusaad.com/macos-forensics-spotlight-challenge/
* https://ahmedmusaad.com/pinned-messages-in-slack-channels/
* https://twitter.com/twostraws/status/1328700910546132993?s=24
* https://www.reddit.com/r/hardware/comments/jvq3do/the_fallacy_of_synthetic_benchmarks/
* https://www.reddit.com/r/privacy/comments/jvgwg2/its_all_a_big_misunderstanding_says_apple_after/
* https://news.ycombinator.com/item?id=25109724 # Apple VPN Bypass
* https://news.ycombinator.com/item?id=25112768 # BigSur Update Issue
* https://www.bejarano.io/hardening-macos/

### iCloud Self-Hosted Relay:

* https://news.ycombinator.com/item?id=31387019
* https://support.apple.com/en-au/HT212614

-----

# Post Exploitation:

```

# screencapture

-c      Force screen capture to go to the clipboard.
-b      Capture Touch Bar, only works in non-interactive modes.
-C      Capture the cursor as well as the screen.  Only allowed in non-interactive modes.
-d      Display errors to the user graphically.
-i      Capture screen interactively, by selection or window.  The control key will cause the screen shot to go to the clipboard.  The
space key will toggle between mouse selection and window selection modes.  The escape key will cancel the interactive screen shot.
-m      Only capture the main monitor, undefined if -i is set.
-D      <display> Screen capture or record from the display specified. 1 is main, 2 secondary, etc
-o      In window capture mode, do not capture the shadow of the window.
-p      Screen capture will use the default settings for capture. The files argument will be ignored.
-M      Open the taken picture in a new Mail message.
-P      Open the taken picture in a Preview window or QuickTime Player if video.
-I      Open the taken picture in Messages.
-B      <bundleid> Open in the app matching bundleid.
-s      Only allow mouse selection mode.
-S      In window capture mode, capture the screen instead of the window.
-J      <style> Sets the starting style of interfactive capture "selection","window","video".
-t      <format> Image format to create, default is png (other options include pdf, jpg, tiff and other formats).
-T      <seconds> Take the picture after a delay of <seconds>, default is 5.
-w      Only allow window selection mode.
-W      Start interaction in window selection mode.
-x      Do not play sounds.
-a      Do not capture attached windows.
-r      Do not add screen dpi meta data to captured file.
-l      <windowid> Captures the window with windowid.
-R      <rectangle> Capture rectangle using format x,y,width,height.
-v      Capture video recording of the screen.
-V      <seconds> Capture video recording of the screen for the specified seconds.
-G      <id> Captures audio during a video recording using audio source specified by id.
-g      Captures audio during a video recording using default input.
-k      Show clicks in video recordings.
-U      Show interactive toolbar in interactive mode.
-u      Present UI after screencapture is complete. Files passed to commandline will be ignored.
```

-----

```
  say

  Converts text to speech.
  More information: https://ss64.com/osx/say.html.

  - Say a phrase aloud:
    say "I like to ride my bike."

  - Read a file aloud:
    say --input-file=filename.txt

  - Say a phrase with a custom voice and speech rate:
    say --voice=voice --rate=words_per_minute "I'm sorry Dave, I can't let you do that."

  - List the available voices (different voices speak in different languages):
    say --voice="?"

  - Say something in Polish:
    say --voice=Zosia "Litwo, ojczyzno moja!"

  - Create an audio file of the spoken text:
    say --output-file=filename.aiff "Here's to the Crazy Ones."
```