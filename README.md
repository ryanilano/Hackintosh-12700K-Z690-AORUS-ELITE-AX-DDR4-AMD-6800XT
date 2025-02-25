<img src="https://i.imgur.com/IfsTVAq.png" height="150" title="HackintoshLogo">

# macOS Ventura - Hackintosh

**Latest working macOS**: 13.2.1 (22D68)

**Current OpenCore**: [0.9.0 MOD](https://gitee.com/btwise/OpenCore_NO_ACPI) ([binaries](https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases))

## Hardware:
- **CPU**: Intel 13900k @ 5.8GHz
	- **Cooling**: 
		- Noctua NH-D15 (with Thermal Grizzly Kryonaut) 
		- 6x Noctua Fans around the case for airflow
- **Motherboard**: Gigabyte Z690 AORUS ELITE AX DDR5
- **GPU**: 
	- AMD Radeon RX 6900 XT (Main)
	- AMD Radeon RX 550 4GB LP (PowerColor Red Dragon - To be used when I switch to 7900XTX or 4090)
- **WiFi/Bluetooth**: Fenvi T919 with wired antennas
- **Ethernet**: Realtek RTL8125B PCI Express 2.5 Gigabit Ethernet
- **RAM**: 64GB @ 5400 MHz DDR5
- **NVME SSD**: 
	- 500GB WD BLACK SN850 Gen.4 NVMe PCIe SSD (macOS)
	- 500GB Samsung 980 PRO Gen.4 NVMe PCIe SSD (Windows)
	- 500GB Kingston A2000 Gen.3 NVMe PCIe SSD (Linux)
- **SATA SSD**: 
	- 4TB Samsung Evo 860 SATA SSD (shared with macOS, Windows and Linux - formatted as exFAT)
- **Power Supply**: Seasonic Prime PX - 1000W
- **PC Case**: NZXT H710 (important because front usb ports are mapped)

Full hardware specs and prices on [PCPartPicker](https://pcpartpicker.com/user/iphonewsro/saved/zgh4sY)

**SMBIOS**: iMacPro1,1

The system triple boots Windows 11 and Ubuntu Mate

## Tools
Don't be an idiot and use these great tools instead of wasting your time with propertree or other plist editors:
- [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) - easy `config.plist` management
  - [OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig) - alternative
- [Hackintool](https://github.com/headkaze/Hackintool/releases) - debug and map USB ports

> **Warning** 
> 
> Use the [modded OpenCore version](https://gitee.com/btwise/OpenCore_NO_ACPI) to prevent Windows thinking you're running in BootCamp and creating multiple issues around ACPI. Why isn't this the default OC behaviour is beyond me.

## Get it running
1. Make sure to update your BIOS, disable CSM support and secure boot, enable XHCI Hand-off (for Airdrop/Continuity/Sidecar) and enable XMP.
2. Create an macOS Ventura USB-Installer Stick, install OpenCore and copy my EFI folder ([how?](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/))
3. Generate a new serial number, motherboard id, ROM (that's your motherboard's mac address without dots) and SMUUID (make sure serial number is **invalid** in order to iMessage/Facetime to work) ([how?](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo))
4. Boot the new macOS partition
5. Copy the EFI to the local disk

> **Note** 
> 
> Enable HiDPI Display settings by running `sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true` and rebooting the PC

Here are some [tips and tricks](https://github.com/5T33Z0/OC-Little-Translated/tree/main/A_Config_Tips_and_Tricks) and the full [OpenCore Documentation](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html)

## What works
- macOS Ventura
- WiFi and Bluetooth + Airdrop + Sidecar + Continuity (OOB via Fenvi T919)
- Audio
- HDMI/DP (with VRR)
  - Note that the RX550 can only output to HDMI
- Most USB ports (Capped at macOS limit of 15)
- Everything iCloud related (Drive, iMessage, Facetime, unlock with Apple Watch, etc)
- Intel Quick Sync (if you enable iGPU in BIOS)
- Temperature monitoring
- Resizable Bar Support (enable Above 4G Decoding in BIOS)
- Shutdown/Reboot/Update to newer macOS builds over time

## What doesn't work
- Returning from sleep won't wake up the display. You need to re-plug the DP or HDMI cable. This is probably because of the RX550 hack.

> **Note** 
> 
> The RX550 hack can be disabled by removing the `-radcodec` boot arg and disabling the `550.aml` ACPI patch.

## Port mapping
I mapped both USB 3.0 ports and USB-C port of the case (front), all USB 2.0 ports, another 3 USB 3.0 ports (first ones coming down) + USB-C port on motherboard. Create your own mapping on Windows using [USBToolBox](https://github.com/USBToolBox/tool)

## Xcode Benchmark
This setup beats the Mac Studio 2022 (M1 Ultra 20-core) and the Mac Mini 2023 (M2 Pro) on [Xcode compiling time](https://github.com/devMEremenko/XcodeBenchmark/pull/369). This hackintosh is the best developer machine possible, even beating M2 Pro Macs.

## Kexts
- Lilu
- Whatevergreen
- AppleALC
- VirtualSMC + SMCProcessor + SMCSuperIO
- CpuTopologyRebuild
- RestrictEvents
- CpuTscSync
- USBPorts (USBToolBox + USBMap)
- NVMeFix
- LucyRTL8125Ethernet

## Drivers
- OpenCanopy
- OpenRuntime
- OpenLinuxBoot (optional)
- OpenHfsPlus (optional)
- AudioDxe (optional, for boot chime)

![neofetch](https://i.imgur.com/Btx4WPB.png)

## Thanks/Credits
- [Luchina Gabriel](https://github.com/luchina-gabriel)
- [MaLd0n](https://www.olarila.com/)
- insanelymac
- tonymacx86

**Fuck /r/Hackintosh mods for not allowing EFI sharing, forcing people to use propertree and other trash instead of great GUI apps**
