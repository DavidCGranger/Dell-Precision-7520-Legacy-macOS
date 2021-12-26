# Dell-Precision-7520-Legacy-macOS-OpenCore
 
### Before you give this EFI a try, make sure you read [this](#Generating-your-own-serial-and-Editing-ROM)!

This repo includes an OpenCore EFI for the Dell Precision 7520 (i7-6820HQ, Skylake) for legacy
Versions of macOS, currently only High Sierra, with a little luck all the way from
El Capitan to Big Sur, Monterey being supported mainline.

Testing on:

Model | Dell Precision 7520
------------- | ---------------
CPU | Intel Core i7-6820HQ
iGPU | Intel HD Graphics 530
dGPU | NVIDIA Quadro M2200
RAM | 32 GB DDR4
WiFi | Intel® Dual Band-Wireless-AC 8265

## What works?
currently not completely known
 - WiFi
 - Trackpad
 - USB
 - Boot
 - Keyboard
 - Camera (should work, not being tested actively)
 - USB-C (should work, not being tested actively)

## What doesn't work?
currently not completely known
-Bluetooth
-Card Reader

## BIOS settings

- Virtualization Support: Enabled
- SATA Mode: AHCI
- Thunderbolt: Disabled
- TPM: Disabled
- Legacy Mode: Disabled
- (for Nvidia) Switchable Graphics: Disabled

## How to install

Download this repo and place the EFI folder into your internal drive's EFI partition... That's it.

## How to Install macOS

There are two ways you can make a USB installer:

1. Have a working install of macOS, download the Installer from the App Store, then make a bootable Installer with `createinstallmedia` by using this command in Terminal `sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`

2. If you are using Windows, use [macrecovery.py](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html) from the offical OpenCore release package.

After you have created a bootable Installer, copy the EFI folder to the EFI partition of the installer drive and install as usual (GUID Partiton Map; APFS). After the installation, mount the EFI partition of the installed OS and copy the EFI folder to its partition.

## Generating your own serial and Editing ROM

Use GenSMBIOS (https://github.com/corpnewt/GenSMBIOS) to generate a serial for MacBookPro13,3

use PlistEdit Pro or any decent plist editor to manually enter the details in the following sections of the config (as shown in the video): (SystemSerialNumber, MLB, and UUID)

https://user-images.githubusercontent.com/59102649/116117179-3ea51200-a6bc-11eb-8a18-a03f7bb5bf1d.mp4

You should also put in your ethernet adapter's MAC address into the ROM section.

## Credits

* [acidanthera](https://github.com/acidanthera) (for OpenCore and the kexts)
* [dortania](https://dortania.github.io/OpenCore-Install-Guide/) (for their awesome guide)
* [OpenIntelWireless](https://github.com/OpenIntelWireless) (for Intel WiFi and Bluetooth)
* [blankmac](https://github.com/blankmac/AlpsHID) (for the APLS I2C TouchPad kext)
