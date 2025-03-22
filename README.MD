## Custom enhanced version of magisk allowing to patch unsupported devices

Some android devices have boot structures that dont comply the android standards designed by Google and magisk doesn't support them. This is the case of the Xiaomi Redmi Pad SE 8.7 (codenames "flare" and "spark") and more.

This custom version does, and also contains multiple enhancements compared to the original version: lists all ramdisk in the selected file, checks that it contains at least one, checks if there is at least one init binary to patch inside one of the ramdisks, auto-selection of the ramdisk to patch if multiple are present, more verbose logs, ...

## Disclaimer

This custom version is unofficial so if you have issues with it ask here : https://github.com/NeutroGe/Magisk_for_unsupported_devices/issues but not on the official Magisk github.

I tested it on my own device and on boot images of other devices and it worked well. However you are using it at your own risks, which shouldn't be too great if you know what you are doing, at worst reflash the original boot image and that's it.

But if you do something wrong by mistake and you brick your device using it, it's on you (same as with the original version of magisk).

## Usage for regular devices (on which the regular version of magisk already work)

Download the apk file from the "releases" section on the right of this page

Usage is the same as described on the official magisk website: https://topjohnwu.github.io/Magisk/install.html

## How to know if your device is unsupported by the official version of magisk:

 - Your device fastboot firmware do not contain an init_boot.img image,

 - Your device fastboot firmware do not contain a recovery.img image,

 - your device fastboot firmware has a boot.img image, but patching it with the official magisk app doesn't root your device. There are no errors in the patching process, but the system is still not rooted after flahsing the patched boot.img image.

If the conditions are met, it means your device could be non compliant to android standards and the boot ramdisk could be located on another image than boot.img, init_boot.img or recovery.img.

In this case, follow the instructions described in the official magisk guide https://topjohnwu.github.io/Magisk/install.html , but instead of using a boot.img, init_boot.img or recovery.img image, use the vendor_boot.img image, or any other image that could potentially contain the ramdisk which has the init binary inside it (which needs to be patched by magisk to root, among other things).

If the app found something to patch from the image file you selected it will do so, but it doesn't mean that booting or rooting from this modified image will always work. You might have to try different images until you find one that works.

## Custom modifications

If you want to modify the boot_patch.sh script used for this app and generate your own custom version of magisk, the easiest way is to download an APK editor file (i used this one: https://github.com/PatrickAlex2019/ApkEditor ) to switch the boot_patch.sh script contained inside the APK by your own.

This could be useful if the images contain ramdisks with unconventional names for example. In that case you could modify the script to include these names to the names of ramdisks the app already tries to patch.

## Credits

All the contributors of the official magisk app https://github.com/topjohnwu/Magisk , especially https://github.com/yujincheng08

The kind people who helped me figure out all of this on XDA forum https://xdaforums.com/t/magisk-general-support-discussion.3432382/page-2991  - pndwal - J.Michael - badabing2003 - DiamondJohn - Nergal di Cuthah - ...
