# Gathering files
Last edited: January 30, 2020

This section is for gathering miscellaneous files for booting macOS, we do expect you to know your hardware well before starting and hopefully made a Hackintosh before as we won't be deep diving in here.

## Firmware Drivers

These are the drivers used for OpenCore, for the majority of systems you only need 3 .efi drivers to get up and running:

* [ApfsDriverLoader.efi](https://github.com/acidanthera/AppleSupportPkg/releases)
  * Needed for seeing APFS volumes.
* [VboxHfs.efi](https://github.com/acidanthera/AppleSupportPkg/releases) **or** [HfsPlus.efi](https://cdn.discordapp.com/attachments/606452360495104000/633621011887292416/HFSPlus.efi)
  * Needed for seeing HFS volumes. **Do not mix HFS drivers**
* [FwRuntimeServices.efi](https://github.com/acidanthera/OpenCorePkg/releases)
  * Replacement for [AptioMemoryFix.efi](https://github.com/acidanthera/AptioFixPkg), used for patching boot.efi for NVRAM fixes and better memory management.

For legacy users:

* [AppleUsbKbDxe.efi](https://github.com/acidanthera/OpenCorePkg/releases)
   * Used for OpenCore picker on **legacy systems running DuetPkg**, [not recommended and even harmful on UEFI(Ivy Bridge and newer)](https://applelife.ru/threads/opencore-obsuzhdenie-i-ustanovka.2944066/page-176#post-856653)
* [NvmExpressDxe.efi](https://github.com/acidanthera/OpenCorePkg/releases)
   * Used for Haswell and older when no NVMe driver is built into the firmware
* [XhciDxe.efi](https://github.com/acidanthera/OpenCorePkg/releases)
   * Used for Sandy Bridge and older when no XHCI driver is built into the firmware


For a full list of compatible drivers, see 11.2 Properties in the [OpenCorePkg Docs](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf). These files will go in your Drivers folder in your EFI

## Kexts

A kext is a **k**ernel **ext**ension, you can think of this as a driver for macOS, these files will go into the Kexts folder in your EFI

All kext listed below can be found pre-compiled in the [Kext Repo](http://kexts.goldfish64.com/). Kexts here are compiled each time there's a new commit.

**Must haves**:

* [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases)
  * Emulates the SMC chip found on real macs, without this macOS will not boot
  * Alternative is FakeSMC which can have better or worse support, most commonly used on legacy hardware.
* [Lilu](https://github.com/vit9696/Lilu/releases)
  * A kext to patch many processes, required for AppleALC and WhateverGreen and recommended for VirtualSMC

**VirtualSMC Plugins**:

* SMCProcessor.kext
  * Used for monitoring CPU temperature
* SMCSuperIO.kext
  * Used for monitoring fan speed
* SMCLightSensor.kext
  * Used for the ambient light sensor on laptops
* SMCBatteryManager.kext
  * Used for measuring battery readouts on laptops, **requires your battery to be setup. Do not use before battery patching**

**Graphics**:

* [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases)
  * Used for graphics patching, all GPUs benefit from this kext.

**Audio**:

* [AppleALC](https://github.com/vit9696/AppleALC/releases)
  * Used for AppleHDA patching, used for giving you onboard audio. AMD 15h/16h may have issues with this and Ryzen/Threadripper systems rarely have mic support

**Ethernet**:

* [IntelMausiEthernet](https://github.com/Mieze/IntelMausiEthernet)
  * Required for Intel NICs
* [AtherosE2200Ethernet](https://github.com/Mieze/AtherosE2200Ethernet)
  * Required for Atheros and Killer NICs
* [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X)
  * Required for Realtek NICs

**USB**:

* [USBInjectAll](https://bitbucket.org/RehabMan/os-x-usb-inject-all/downloads/)
  * Used for injecting intel USB controllers, H370, B360, H310 and X79/X99/X299 systems will likely need [XHCI-unsupported](https://github.com/RehabMan/OS-X-USB-Inject-All) as well.

**Trackpad**:
* [VoodooI2C](https://github.com/alexandred/VoodooI2C/)

**Keyboard**:
* [VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2/)

**WiFi and Bluetooth**:

* [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup)
  * Used for patching non-Apple Broadcom cards, **will not work on intel, Killer, Realtek, etc**
* [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM)
  * Used for uploading firmware on broadcom bluetooth chipset, required for all non-Apple Airport cards.
  * To be paired with BrcmFirmwareData.kext
    * BrcmPatchRAM3 for 10.14+ (must be paired with BrcmBluetoothInjector)
    * BrcmPatchRAM2 for 10.11-10.14
    * BrcmPatchRAM for 10.10 or older

**Extra's**:

* [NVMeFix](https://github.com/acidanthera/NVMeFix/releases)
   * Used for fixing power management and initialization on non-Apple NVMe, requires macOS 10.14 or newer
* [NoTouchID](https://github.com/al3xtjames/NoTouchID)
   * Required for MacBookPro13,x+, helps fix lag at login and authentication dialogs


Please refer to [Kexts.md](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Kexts.md) for a full list of supported kexts

## SSDTs

So you see all those SSDTs in the AcpiSamples folder and wonder whether you need any of them. For us, we will be going over what SSDTs you need in **your specific ACPI section of the config.plist**, as the SSDTs you need are platform specific. With some even system specific where they need to be configured and you can easily get lost if I give you a list of SSDTs to choose from now. 

[Getting started with ACPI](/extras/acpi.md) has an extended section on SSDTs including compiling them on different platforms.

# Now head to your specific CPU section to setup your config.plist

**Intel Config.plist**

* [Ivy Bridge](/config.plist/ivy-bridge.md)
* [Haswell](/config.plist/haswell.md)
* [Broadwell](/config.plist/broadwell.md)
* [Skylake](/config.plist/skylake.md)
* [Kaby Lake](/config.plist/kaby-lake.md)
* [Coffee Lake(8th Gen)](/config.plist/coffee-lake-8th-gen.md)
* [Coffee Lake(9th Gen)](/config.plist/coffee-lake-9th-gen.md)
* [Comet Lake](/config.plist/comet-lake.md)

