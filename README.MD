## Custom version of magisk allowing to patch uncompliant android devices vendor_boot images

Some android devices have boot structures that are non compliant with the android standards: the boot partition contains only the kernel, there is no init_boot partition, no recovery partition, and the vendor_boot partition contains init_boot.cpio (with possibly additional cpios like recovery.cpio and ramdisk.cpio).

This is the case of the Xiaomi Redmi Pad SE 8.7 (codenames "flare" and "spark") and probably more devices.

If you are reading this as a developper working on these devices or another one which is non compliant in the same way, please do the necessary changes so that the device becomes compliant and dont only rely on this tool as a workaround please.

The official magisk app do not support non compliant devices, thus trying to patch boot_vendor.img of these non compliant devices will have no effect (the content of the result "magisk_patched-xxx" file will be identical to the original file, so flashing it will change nothing).

## Disclaimer - UNOFFICIAL AND EXPERIMENTAL

The following rooting method by patching the vendor_boot.img image is not officially supported by magisk, so please dont ask them for help about this in the official magisk github, thank you. 

Also it's experimental, so it might not work. If you know what you are doing, it shouldn't brick your device, worst case scenario you will have to reflash the original vendor_boot.img and that's it, but use at your own risk. I'm not responsible if you brick your device because you used this tool.


## How to know if your device could be non compliant:

 - Your device bootloader must be unlocked. Dont try otherwise or you might brick it.

 - Your device fastboot firmware do not contain an init_boot.img image,

 - Your device fastboot firmware do not contain a recovery.img image,

 - your device fastboot firmware has a boot.img image, but patching it with the official magisk app doesn't root your device. There are no errors in the patching process, but the system is still not rooted after it.

If all the 4 above conditions are not met, your device is not concerned and trying to patch your vendor_boot.img will not work, so do not try and stop here.

If the conditions are met, it means your device could be non compliant and the boot ramdisk could be not located on your vendor_boot.img image, so try what follows.

## Usage

Download the latest magisk.apk stable release file and modify it to replace the file magisk.apk/assets/boot_patch.sh by the one you can download above in the "/scripts" folder.

You can use the app named "APK Editor" to do so, or other utilities you find elsewhere (you cant directly inject it with a zip file manager as the signature of the apk will be broken and you wont be able to install it).

After that, install this modified magisk apk on your device (delete the magisk app before if it's already installed), transfer your vendor_boot.img to your device and use the modified magisk app to patch it by using the “Select and Patch a File” option on the patched magisk app.

Retreive the generated "magisk_patched_xxx.img" image file then reboot your unrooted device to bootloader/fastboot using "adb reboot bootloader" and flash the patched image by using "fastboot flash vendor_boot <name of your magisk patched file.img>" then reboot your device with "fastboot reboot".

If everything goes well the next time you start the magisk app you should see that the device is now rooted!
