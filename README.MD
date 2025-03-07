## How to root an android device by patching the boot_vendor.img image in some specific cases

This is the case of the Xiaomi Redmi Pad SE 8.7 - codenames "flare" and "spark", and probably more.


## Disclaimer - UNOFFICIAL AND EXPERIMENTAL

The following rooting method by patching the vendor_boot.img image is not officially supported by magisk, so please dont ask them for help about this, thank you. 

Also it's an experimental rooting method, so it might not work. If you know what you are doing, it shouldn't brick your device, worst case scenario you have to reflash the original vendor_boot.img and that's it, but use at your own risk.


## How to know if your device might fall into that category:

 - Your device bootloader must be unlocked. Dont try otherwise or you might brick it.

 - Your device fastboot firmware do not contain an init_boot.img image,

 - your device fastboot firmware has a boot.img image, but patching it with magisk doesn't root your device. There are no errors in the patching process, but the system is still not rooted after it.

 - Your device fastboot firmware has a boot_vendor.img image.

If all the 3 above conditions are not met, your device is not concerned so no need to waste time on it, sorry.

If the conditions are met, there are still more you need to check, keep reading below.


## Unpacking boot.img and vendor_boot.img

Use https://github.com/svoboda18/magiskboot for windows or https://topjohnwu.github.io/Magisk/tools.html for linux to unpack your boot.img and vendor_boot.img images.

If your boot.img image contains only a file named "kernel" and your vendor_boot.img has the following structure:

Root -> vendor_ramdisks (folder)
           -> init_boot.cpio
           -> ramdisk.cpio
           -> recovery.cpio

    -> dtb

Then this modified "boot_patch.sh" script might be able to patch your vendor_boot.img image to root your device!


## Usage

### From an already rooted android device

This is the easiest way. Download the latest magisk.apk stable release file and modify it to replace the file magisk.apk/assets/boot_patch.sh by the one you can download above in the "/scripts" folder.

You can use the app named "APK Editor" to do so, or other utilities you find elsewhere (you cant directly inject it with a zip file manager as the signature of the apk will be broken and you wont be able to install it).

After that, installed this modified magisk apk on the rooted device (delete the magisk app before if it's already installed), transfer your vendor_boot.img to the rooted device and use the modified magisk app to patch it by using the “Select and Patch a File” option on the patched magisk app.

Retreive the generated "magisk_patched_xxx.img" image file then reboot your unrooted device to bootloader/fastboot using "adb reboot bootloader" and flash the patched image by using "fastboot flash vendor_boot <name of your magisk patched file.img>" then reboot your device with "fastboot reboot".

If everything goes well the next time you start the magisk app you should see that the device is now rooted!

However, magisk will say you have to reinstall it because the patch was built on a different device, so some parameters are off.

To correct this you need to repeat the patching process from your own device, and after flashing the patched vendor_boot generated from your own device, there should be no more errors :)


### From a PC on an linux environment

If you dont have an already rooted android device available you need to use a PC on linux to patch the boot_vendor.img file. I used Ubuntu 22.04 LTS on a VM for this, but any recent popular distribution should do.

Here's how:

 - download the latest magisk.apk official release file and extract the following files in the same folder:

   - \lib\x86_64\libinit-ld.so -> rename to init-ld

   - \lib\x86_64\libmagiskboot.so -> rename to magiskboot

   - \lib\x86_64\libmagisk.so -> rename to magisk

   - \assets\stub.apk

   - \assets\chromeos (whole folder)

 - add the boot_patch.sh file from the /script folder above on this repository in the same folder

 - add the original vendor_boot.img file from your device official firmware/rom

After this run the boot_patch.sh script with the command "bash ./boot_patch.sh vendor_boot.img"

This will generate a patched vendor_boot.img file that you can flash to your device as explained before. If it works then magisk will tell you that it needs to be reinstalled because it wasn't generated on the device itself, so you need to re-generate a patched vendor_boot.img from your rooted device with a modified magisk.apk as explained earlier, flash it, and you're good to go :)

