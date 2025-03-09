## Custom version of magisk allowing to patch unsupported devices

Some android devices have boot structures that dont respect the android standards designed by Google and magisk doesn't support them. This custom version does.

This is the case of the Xiaomi Redmi Pad SE 8.7 (codenames "flare" and "spark") and more.

## Disclaimer

This custom version is unofficial so if you have issues with it ask here : https://github.com/NeutroGe/Magisk_for_unsupported_devices/issues but not on the official Magisk github.

I tested it on my own device and on boot images of other devices and it worked well. However you are using it at your own risks, which shouldn't be too great if you know what you are doing, at worst reflash the original boot image and that's it. But if you do something wrong by mistake and you brick your device using it, it's on you.

## How to know if this custom version applies to your device:

 - YOUR DEVICE BOOTLOADER MUST BE FULLY UNLOCKED. IF IT'S NOT, DO NOT TRY TO USE THIS TOOL OR YOU MIGHT BRICK IT.

 - Your device fastboot firmware do not contain an init_boot.img image,

 - Your device fastboot firmware do not contain a recovery.img image,

 - your device fastboot firmware has a boot.img image, but patching it with the official magisk app doesn't root your device. There are no errors in the patching process, but the system is still not rooted after flahsing the patched boot.img image.

If the 3 above conditions are not met your device should be compatible with the official version of magisk which you should use instead of this one.

If the conditions are met, it means your device could be non compliant and the boot ramdisk could be not located on your vendor_boot.img image, so try what follows.

## Usage

Download the modified magisk app on the right of this page from the "release" section.

Follow the instructions described in the official magisk guide https://topjohnwu.github.io/Magisk/install.html , but instead of using a boot.img, init_boot.img or recovery.img image, use the vendor_boot.img image, or any other image that could contain the init_boot ramdisk).

The app will list any non compliant ramdisk contained in the image file you selected, search if one of them is the init_boot ramdisk, and patch it if it is.

If the input file contains an init_boot ramdisk, after flashing the patched image file to the partition of the same name as the input file you selected (so for example, if using vendor_boot.img as input, flash the patched file to the "vendor_boot" partition), if everything goes well your device should now be rooted!

If that's the case and your device model is not listed here, please create an issue on this github page and write down your device model (be as specific as possible) so that i can add it to the list :)

Note that this app should also work on regular compliant device images files the same way the official app does (with a bit more error checking).

## Other infos

If you want to modify the boot_patch.sh script used for this app and generate your own custom version of magisk, the easiest way is to download an APK editor file (i used this one: https://github.com/PatrickAlex2019/ApkEditor ) to switch the boot_patch.sh script contained inside the APK by your own.

## Credits

All the contributors of the official magisk app https://github.com/topjohnwu/Magisk , especially https://github.com/yujincheng08

The kind people who helped me figure out all of this on XDA forum https://xdaforums.com/t/magisk-general-support-discussion.3432382/page-2991  - pndwal - J.Michael - badabing2003 - DiamondJohn - Nergal di Cuthah - ...
