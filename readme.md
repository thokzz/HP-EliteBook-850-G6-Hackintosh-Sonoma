# HP EliteBook 850 G6 Hackintosh

![System Information](https://github.com/thokzz/HP-EliteBook-850-G6-Hackintosh-Sonoma/blob/main/asset/Screenshot.png)

![Desktop Environment](https://github.com/thokzz/HP-EliteBook-850-G6-Hackintosh-Sonoma/blob/main/asset/Screenshot2.png)

This repository contains the necessary EFI files and instructions to install and run macOS on the HP EliteBook 850 G6 with an Intel i7 8th Generation processor.

## Hardware Specifications

| Component | Details |
|-----------|---------|
| Model | HP EliteBook 850 G6 |
| CPU | Intel Core i7 8th Generation |
| GPU | Intel UHD Graphics 630 |
| RAM | Stock configuration |
| Audio | ALC285 (layout-id: 18) |
| Wi-Fi | Intel Wi-Fi |
| Bluetooth | Intel Bluetooth |
| Ethernet | Intel Ethernet Controller |
| Touchpad | I2C HID and PS/2 |

## What Works

✅ CPU Power Management  
✅ Intel UHD Graphics 630 with full acceleration  
✅ Display (internal and HDMI output)  
✅ Audio (internal speakers, headphone jack)  
✅ Wi-Fi (using AirportItlwm.kext)  
✅ Bluetooth  
✅ USB ports (properly mapped with USBToolBox)  
✅ Trackpad (with gestures)  
✅ Keyboard and function keys  
✅ Battery status and power management  
✅ Sleep/Wake  
✅ Brightness control (with hotkeys)  
✅ Ethernet  
✅ NVMe storage  
✅ Integrated webcam 
✅ iCloud, Xcode, Appstore

## Not working
Facetime and imessage only working in Monterey
Built in Mic Not working

## macOS Compatibility

This EFI configuration has been tested with:
- macOS Sonoma
- macOS Ventura
- macOS Monterey

## Installation Guide

### Prerequisites

- A USB drive (minimum 16GB)
- Access to a macOS machine or VM to create the installer
- [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/) (optional, for EFI editing)

### Creating the macOS Installer

1. Download macOS from the App Store
2. Format your USB drive with GUID Partition Map and macOS Extended (Journaled)
3. Use the `createinstallmedia` command to create the installer:
   ```
   sudo /Applications/Install\ macOS\ [Version].app/Contents/Resources/createinstallmedia --volume /Volumes/[USB Volume Name]
   ```

### EFI Setup

1. Mount the EFI partition of your USB drive
2. Copy the entire EFI folder from this repository to the EFI partition
3. (Optional) Generate new SMBIOS information using OpenCore Configurator or GenSMBIOS
   - This build uses MacBookPro16,3 SMBIOS

### BIOS Settings

Before installation, configure these settings in BIOS:

1. Disable Secure Boot
2. Enable UEFI Boot
3. Disable VT-d
4. Disable TPM Security
5. Set DVMT Pre-allocated to 64MB
6. Disable Fast Boot
7. Set Boot Mode to UEFI
8. Disable Intel SGX

### Installation

1. Boot from the USB installer
2. Select "macOS Installer" from the OpenCore boot menu
3. Follow the standard macOS installation process
4. After installation, boot into macOS
5. Mount the EFI partition of your internal drive and copy the EFI folder from your USB

## Post-Installation

### Fixing Sleep Issues

If you encounter sleep issues, run these commands in Terminal:

```
sudo pmset -a hibernatemode 0
sudo pmset -a autopoweroff 0
sudo pmset -a standby 0
```

### Fixing iServices

If iMessage, FaceTime, or other Apple services aren't working:

1. Generate a new SMBIOS with valid serial numbers
2. Make sure your system clock is set correctly
3. Sign out of iCloud and sign back in

## OpenCore Configuration

This build uses OpenCore 0.9.x bootloader with the following components:

### ACPI
- SSDT-AWAC.aml
- SSDT-BATT.aml
- SSDT-EC-USBX-LAPTOP.aml
- SSDT-PLUG-DRTNIA.aml
- SSDT-PMC.aml
- SSDT-PNLF-CFL.aml
- SSDT-XOSI.aml
- ssdt-rmne.aml

### Kexts
- Lilu.kext (v1.7.0)
- VirtualSMC.kext (v1.3.5)
- USBToolBox.kext (v1.1.1)
- UTBMap.kext (v1.1)
- BrcmPatchRAM3.kext (v2.6.9)
- IntelBluetoothFirmware.kext (v2.4.0)
- NVMeFix.kext (v1.1.2)
- VoodooPS2Controller.kext (v2.3.7)
- WhateverGreen.kext (v1.6.9)
- VoodooI2C.kext (v2.9.1)
- VoodooI2CHID.kext
- AppleALC.kext (v1.9.4)
- AirportItlwm.kext (v2.3.0)
- BlueToolFixup.kext (v2.6.9)
- BrightnessKeys.kext (v1.0.3)
- ECEnabler.kext (v1.0.5)
- IntelBTPatcher.kext (v2.4.0)
- IntelMausi.kext (v1.0.8)
- SMCBatteryManager.kext (v1.3.5)

### Drivers
- OpenCanopy.efi
- OpenHfsPlus.efi
- OpenRuntime.efi
- ResetNvramEntry.efi

## Graphics Configuration

The Intel UHD Graphics 630 is configured with:
- AAPL,ig-platform-id: 00009B3E
- device-id: 9B3E0000
- Framebuffer patches for proper display output

## USB Configuration

USB ports are properly mapped using USBToolBox with the following features:
- All USB 3.0 and 2.0 ports working
- Internal Bluetooth and webcam recognized

## Audio Configuration

Audio is working through AppleALC with:
- layout-id: 18
- Proper mic and speaker functionality

## Credits and Thanks

- [Acidanthera](https://github.com/acidanthera) for OpenCore and most of the kexts
- [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [USBToolBox](https://github.com/USBToolBox/kext)
- [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C)
- The entire Hackintosh community for documentation and support


## Warning

This EFI configuration is specifically tailored for the HP EliteBook 850 G6 with an i7 8th generation processor. Using it on different hardware may require modifications. Always back up your data before attempting to install macOS on non-Apple hardware.
