# Gigabyte Designaire Z390 - OpenCore - macOS Catalina

This guide is using macOS Catalina 10.15.4 (19E287), and OpenCore 0.5.7 with integrated boot selector UI. Currently, debug and verbose mode are disabled. If you have exactly the same hardware as I do, this is probably not an issue. Otherwise, it might be helpful to use the `DEBUG` releases of OpenCorePkg and AppleSupportPkg rather than `RELEASE` the versions included in this EFI. You should also add the `debug=0x100` and `-v` flags to the boot args, as well as follow [other recommendations](https://desktop.dortania.ml/config.plist/coffee-lake.html#nvram) laid out in the [OpenCore Desktop guide](https://desktop.dortania.ml/).

As always, if this repository is more than a few weeks old when you view it, it would probably behoove you to grab the latest versions of the drivers and kernel extensions used in this EFI.

This EFI is a revision of the [previous Clover EFI](https://github.com/baughmann/Catalina-Gigabyte-Designare-Z390-i9-9900k-EFI) that I posted. Given that OpenCore has a definitive and always-up-to-date installation guide (a much welcome change from Clover), [you should read it](https://dortania.github.io/OpenCore-Desktop-Guide/) in addition to using this EFI.

---

## Hardware
- Gigabyte Designaire Z390
    - Be sure to flash the [latest firmware version](https://www.gigabyte.com/us/Motherboard/Z390-DESIGNARE-rev-10/support#support-dl-bios)! A fantastic beta was released as late as Dec 2019, which is what I use. Just throw it on a USB, boot into the bios, and use Q-Flash to update.
- Intel Core i9 9900K
- AMD Radeon VII 16 GB
- Samsung EVO 970 (NVMe - 1TB)
- Fenvi T919 Bluetooth/Wi-Fi Card

## What works
- Bluetooth & Wi-Fi
- AirDrop and other continuity features
- Audio (rear 3.5mm audio jack works, haven't tested the front)
- Shutdown / Restart / Sleep
- USB 3.0/3/1
- Thunderbold 3 (including charging and hotsqapping)

## What doesn't work
- NVRAM emulation
- Correct pre-kernel screen resolution (OC UI and pre-driver Apple loading screen is slightly stretched)

## What you need to change
I've removed the `MLB`, `SystemSerialNumber`, `SystemUUID` fields under `PlatformInfo` inside the `OC/config.plist` and replaced them with `[REPLACEME]`. You should fill these in to get everything to work properly. Thankfully, the Dortania (OpenCore) guys [mentioned this in their guide](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/iservices.html#generate-a-new-serial). 
- NOTE, I don't personally recommend checking AppleCare for anything I didn't need to do this to get stuff working and find it potentially sketchy to take a legit serial number, especially if you tie it to your Apple account.

## Most important differences from The Official Guide
The primary changes that I remember making that differ from the fantastic [OpenCore Desktop Guide for Coffee Lake](https://dortania.github.io/OpenCore-Desktop-Guide/config.plist/coffee-lake.html) are:
    - boot args `slide=1 alcid=7`
    - Adding my own USB map kext (`USBPorts.kext`) that shuts off the MoBo's built-in Wi-Fi card so that I can use the Fenvi
    - Adding the `HfsPlus.efi` driver

## Important notes about online resources, including The Offical Guide
Since there were some pretty big changes included with OpenCore 0.5.7, a lot of the configurations in `config.plist`s that you see floating around either don't exist or are no longer used. This even affects some of the guide's images, so be sure to *read* the guide, and not just look at the pictures!

## When all else fails, refer to the documentation
OpenCore, unlike Clover, has robust official documentation. While some of it may be confusing, if you follow it 99% of the time you will be OK. Read the docs!
