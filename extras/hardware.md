# Supported hardware

Last edited: January 2, 2020

So this little section is for those who are wanting to know whether their hardware will work in macOS

# Ways to check hardware

* [Speccy](https://www.ccleaner.com/speccy)
* Device Manager
* Product support docs

# CPU Compatibility

* macOS Sierra+ requires a SSE4,1 capable CPU
* Pentiums and some Xeons need CPU ID spoof
* Celerons and mobile pentiums will not work
* AMD CPUs need [kernel patches](https://github.com/AMD-OSX/AMD_Vanilla/tree/opencore)
* 19h AMD CPUs are unsupported(3rd gen threadripper)

# GPU Compatibility

* [See GPU Buyers Guide](https://khronokernel-3.gitbook.io/catalina-gpu-buyers-guide/) for compatible GPUs.

# Motherboard Compatibility

* All AMD and Intel motherboards are supported to a certain extent
* Some intel HEDT systems will need emulated NVRAM
* Some Z370 and Z390 boards have AWAC clocks, these are incompatible with macOS and so will need an RTC fix

# SSD Compatibility

* No eMMC storage
* Samsung PM981 and early 970 Evo Plus models don't work([970 Evo Plus requires a firmware upgrade to work](https://www.tonymacx86.com/threads/do-the-samsung-970-evo-plus-drives-work-new-firmware-available-2b2qexm7.270757/page-14#post-1960453))

# Audio Compatibility

* See the AppleALC wiki for supported codecs: [Supported codecs
](https://github.com/acidanthera/applealc/wiki/supported-codecs)
* Ryzen MIC only works on VoodooHDA and there's no MIC support on 15/16h AMD CPUs

# Networking

See supported chipset on respective drivers:

* [IntelMausiEthernet](https://github.com/Mieze/IntelMausiEthernet)
   * Required for Intel NICs, newer chipsets are based off of I211-AT will need the [SmallTreeIntel82576 kext](https://drive.google.com/file/d/0B5Txx3pb7pgcOG5lSEF2VzFySWM/view?usp=sharing)
* [AtherosE2200Ethernet](https://github.com/Mieze/AtherosE2200Ethernet)
* [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X)

Unsupported ethernet models:
* Realtek L8200A(Only found in Asus boards)
* Realtek RTL8125(2.5Gbe, mostly found on higher end gaming boards)

And see [Wireless Buyers Guide](https://khronokernel-7.gitbook.io/wireless-buyers-guide/) for supported wifi cards. All built in motherboard wireless ccards will not work in macOS, they must be swapped.


