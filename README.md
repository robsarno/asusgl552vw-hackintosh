
# Hackintoshing ASUS GL552VW - macOS BigSur 11
:it:
![Generic badge](https://img.shields.io/maintenance/yes/2021)
![Generic badge](https://img.shields.io/badge/currently_working-brightgreen.svg)
![Generic badge](https://img.shields.io/github/last-commit/robsarno/asusgl552vw-hackintosh)
[![Generic badge](https://img.shields.io/reddit/subreddit-subscribers/hackintosh?style=social)](https://www.reddit.com/r/hackintosh/)
<br>Feel free to contribute.


## :mag: Specs
.| Asus ROG GL552VW
------------ | -------------
**Model**| G552VW
**Motherboard chipset** | Intel HM170
**Processor** | Intel Skylake Core i7-6700HQ CPU, quad-core 2.6 GHz (3.5 GHz TBoost)
**Memory** |16 GB DDR4 2133Mhz (2xDIMMs)
**Storage** |128 GB SSD + 1 TB 2.5″ HDD
**Connectivity** |Wireless : AC Intel 7265 - Lan: Realtek RTL8111 Gigabit ehternet controller
**USB** | 1x USB 2.0, 2x USB 3.0, 1x USB 3.1
**TouchPad** | I2C Elan Touchpad (ELAN1000)
**Screen** |15.6 inch, 1920 x 1080, IPS, non-touch
**Video** |	Integrated Intel HD 530 + Nvidia GTX 960M 2GB

## Getting started
This **ISN'T a full guide, I only provide the EFI folder.** 
<br>For downloading the OS, making the USB installer you have to follow the [Dortania’s OpenCore guide](https://dortania.github.io/OpenCore-Install-Guide/).
<br>I advise you to read that guide carefully to understand what you're going to do. 
<br>The EFI folder provided in this repo contains kexts, SSDTs and config.plist optimized for this notebook.
<br>If the specs don't match you could have bugs.

### Installation
If you want to be sure that my EFI folder contains every needed file:
1. Follow the [Gathering file](https://dortania.github.io/OpenCore-Install-Guide/ktext.html) section on the OpenCore guide.
2. I used pre-built SSDTs [Skylake and Kaby Lake](https://dortania.github.io/Getting-Started-With-ACPI/ssdt-methods/ssdt-prebuilt.html#laptop-skylake-and-kaby-lake)
3. Now check the config.plist [Laptop Skylake](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html)

What you **need to do**:
1. The only this you need (if not you cannot boot) to do is set the SMBIOS for generating serial, board serial and smUUID in config.plist: https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html#platforminfo
2. At this point you have to copy the EFI folder on your USB EFI partition (previously created with OpenCore guide).
3. Continue following the [guide](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html#cleaning-up)

## :fire: Issues 
### :thumbsup: What works 
* Intel HD 530 with graphic acceleration
* Bluetooth
* USB Ports
* Keyboard (no FN keys and backlight atm)
* Ethernet port
* Wifi (with Heliport)
* Battery
* Webcam
* Speakers
* Microphone
* HDMI (with problems)

### :thumbsdown: What doesn't
* Touchpad (need patching, currently working)
* FN keys + backlight (need patching, currently working)
* Nvidia GPU GTX M960 (not supported)

### :exclamation: HDMI issues
If you use external display through HDMI you can:
1.  boot with no HDMI connected and connect after login
2.  boot with HDMI connected, the built-in display'll not work (only backlight). To make it working you have to disconnect HDMI, close and open the lid (now the display will turn on), then connect HDMI.

### :pushpin: To do's
- [ ] Patch touchpad
- [ ] Patch FN keys
- [ ] Patch keyboard backlight
- [ ] Disable Nvidia GPU in SSDTs to preserve battery


## Useful to know

### :books: Guides
* [Dortania's OpenCore guide](https://dortania.github.io/OpenCore-Install-Guide/)
* [Whatevergreen guide](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)
* [AppleALC supported codecs](https://github.com/acidanthera/applealc/wiki/supported-codecs)

### :wrench: Configs
These are requested during the OpenCore official guide to select kexts and configurations in [config.plist](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html).
.| model |. | config.plist
------------ | ------------- |------------- |  -------------
Audio |Conexant CX20751 | AppleALC<br>*layout-id* | 3, 21, 28 (21 is selected in my config.plist)
Graphics|Intel HD530|Whatevergreen<br>*AAPL,ig-platform-id*|0x00001916

boot-args:
* igfxonln=1 :arrow_right: forcing display state on
* -wegnoegpu :arrow_right: disable Nvidia GPU (but currently powered on)

To understand more follow [Whatevergreen guide](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)

### :package: Apps
* [MonitorControl](https://github.com/MonitorControl/MonitorControl/blob/master/README.md)
	* If you can't control your external monitor brightness and audio
* [Hackintool](https://github.com/headkaze/Hackintool)
	* If you want to know more about your system
* [Heliport](https://github.com/OpenIntelWireless/HeliPort)
	* To be able to use wifi with this NIC (Intel 7265)