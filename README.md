# Dell-Precision-7520-legacy-macOS

This repo includes an OpenCore EFI for the Dell Precision 7520 (i7-6820HQ, Skylake) for legacy
Versions of macOS, currently only High Sierra and Big Sur, Big Sur being supported in an EFI supporting both Big Sur and Monterey, and  with a little luck this EFI will support all on Skylake possible macOS Versions.

# High Sierra
 
### Disclaimer
This EFI is currently completely unfinished and has
some major problems. Don't use it, if you don't know what you're doing!
trouble-in-the-macos-installer
### Before you give this EFI a try, make sure you read [this](#Generating-your-own-serial-and-Editing-ROM) and [this](#trouble-in-the-macos-installer)!

Testing on:

Model | Dell Precision 7520
------------- | ---------------
CPU | Intel Core i7-6820HQ
iGPU | Intel HD Graphics 530
dGPU | NVIDIA Quadro M2200 (working with Webdrivers)
RAM | 32 GB DDR4
WiFi | Intel® Dual Band-Wireless-AC 8265 (partially working)

## What works?
currently not completely known
 - Audio
 - Battery readout
 - Boot
 - Brightness Control
 - Ethernet
 - GPU acceleration
 - Keyboard + Trackpad
 - Power Management
 - WiFi
 - Sleep
 - USB
 - Webcam
 - Speaker
 - Trackpoint

## What doesn't work?
currently not completely known
 - Bluetooth
 - Card Reader
 - Headphone Jack

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

## Trouble in the macOS Installer
If USB and the trackpad don't work as intended, here I'm
quickly going over how to fix at least one of these issues.
What's happening, is, AlpsHID, the kext for Magic trackpad Emulation
isn't liking the installer, so you need to disable it temporally
for the install process with a Plist-Editor. I didn't yet find a fix for USB, but
you should be able to install macOS like this and as soon as the install is
complete, everything should work as intended. 

## WiFi
For WiFi to work on High Sierra, you need to install HeliPort, you
can find it here: https://github.com/OpenIntelWireless/HeliPort, and run that
every time you start your computer. It's not optimal, but Airportltlwm caused problems
at least for me. 

## Nvidia Drivers
To install Nvidia Drivers, you need to visit https://www.tonymacx86.com/nvidia-drivers/ on your
Browser and download the latest version and simply install it and restart. If you haven't already
disabled switchable graphics, you need to do it now. 

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
