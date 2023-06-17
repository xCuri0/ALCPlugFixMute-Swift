# ALCPlugFixMute-Swift

(c) 2020 black.dragon74 aka Nick
(c) 2023 xCuri0

macOS daemon to send HD Audio commands (HDA Verbs) to an `IOHDACodecDevice` from user-space.

## Features
- Codeless configuration using a custom `PLIST` file
- Supports sending verbs on system boot/sleep/wake, headset plug/unplug and audio mute/unmute optionally
- Doesn't require `CodecCommander`, `hda-verb` or `alc-verb` to function
- Restore mute status on boot/wake

Note: Requires AppleALC version 1.5.4+ or the patch of commit [61e2bbf](https://github.com/acidanthera/AppleALC/commit/61e2bbfe74bf1c12ebf770ed4a9776a04a7758f2) applied.

## Installing

Download the appropriate version from the [Releases](https://github.com/black-dragon74/ALCPlugFix-Swift/releases/) and extract the zip file.

Open the extracted folder and you will find a `sample.plist` file in there for reference. You need to edit it according to your codec. One you are done, copy the file somewhere safe (it should not be deleted as `ALCPlugFix-Swift` reads the config from it on boot). Also, this is the file you need to drag to the terminal window when `install.sh` asks you to do the same.

Now open the `Terminal.app` and follow the instructions.
```sh
# CD to the downloded directory
cd your_directory_here

# Run the install.sh
./install.sh
```
**Note:** AppleALC version 1.5.5+ require the boot-arg `alcverbs=1` or the property `alc-verbs` to be present on `HDEF` in order for `ALCPlugFix-Swift` to work.

## Mute LEDs
Configurations for HP laptops using Mic1/2/3 for mute LED are included. Only Mic1 has been tested on a HP Notebook 15-ac111tu but the rest should work too. If you do make any additional configurations they can be submitted as a pull request.

You can check [patch_realtek.c](https://github.com/torvalds/linux/blob/master/sound/pci/hda/patch_realtek.c) for how to configure LED when creating a new configuration.

## Building

### From GitHub:

Install Xcode, clone the GitHub repo and enter the top-level directory.  Then:

```sh
xcodebuild -configuration Release
```

## Credits

- [goodwin](https://github.com/goodwin) for original work on Obj-C based ALCPlugFix
- [zen-zhen](https://github.com/zhen-zen) for direct kernelspace connection
- [black-dragon74](https://github.com/black-dragon74) for writing and maintaing this software
- [the-eric-kwok](https://github.com/the-eric-kwok) for restore mute status on boot
