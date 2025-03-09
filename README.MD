## Custom version of magisk allowing to patch unsupported android devices images

Some android devices have boot structures that are non compliant with the android standards. As they do not respect android standards they are not supported by the official version of Magisk. The author of Magisk, https://x.com/topjohnwu works at Google, so it is logical he could have done this because he wants 3rd party vendors to follow standards Google is implementing for android. Or perhaps he just doesn't want to bother to have to deal with all the uncompliant possible structures 3rd party vendors could implement. Or for another unknown reason, after all only him knows, we can only guess.

This is where this unofficial version comes in: it will process any boot image even if their structure is not compliant to android standards. I apologize if it was John Wu's will to not support it because of bad implementation by 3rd party vendors, but I dont think it's fair to the end users we are that we cant root our devices and use them at full capabilities because we unknowingly bought them while they are not compliant to android standards.

This is the case of the Xiaomi Redmi Pad SE 8.7 (codenames "flare" and "spark") and probably more devices.

The official magisk app do not support non compliant devices, thus trying to patch boot_vendor.img of these non compliant devices will have no effect (the content of the result "magisk_patched-xxx" file will be identical to the original file, so flashing it will change nothing).

If you are reading this as a developper working on these devices or another one which is non compliant in the same way, please do the necessary changes so that the device becomes compliant and dont only rely on this tool as a workaround. Thank you.


## Disclaimer - UNOFFICIAL AND EXPERIMENTAL

The following rooting method by patching the vendor_boot.img image is not officially supported by magisk, so please DONT ask them for help about this in the official magisk github, thank you. 

Also it's experimental, so it might not work. If you know what you are doing, it shouldn't brick your device, worst case scenario you will have to reflash the original vendor_boot.img and that's it, but use at your own risk. I'm not responsible if you brick your device because you used this tool.


## How to know if your device could be non compliant:

 - YOUR DEVICE BOOTLOADER MUST BE FULLY UNLOCKED. IF IT'S NOT, DO NOT TRY TO USE THIS TOOL OR YOU WILL BRICK IT.

 - Your device fastboot firmware do not contain an init_boot.img image,

 - Your device fastboot firmware do not contain a recovery.img image,

 - your device fastboot firmware has a boot.img image, but patching it with the official magisk app doesn't root your device. There are no errors in the patching process, but the system is still not rooted after flahsing the patched boot.img image.

If all the 4 above conditions are not met, your device is not concerned and trying to patch your vendor_boot.img will not work, so do not try and stop here.

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
