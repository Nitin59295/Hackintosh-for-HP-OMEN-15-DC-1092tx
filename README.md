# 🚀 Hackintosh EFI – HP Omen 15-dc1092tx (macOS Sequoia 15.1)

This is a working OpenCore EFI configuration for **HP Omen 15-dc1092tx** running **macOS Sequoia 15.1**. It is configured with care to support the Intel iGPU, disable the NVIDIA dGPU, and provide a mostly functional macOS experience on non-Apple hardware.

---

## 🖥️ System Specifications

| Component         | Details                                  |
|------------------|------------------------------------------|
| **Laptop Model** | HP Omen 15-dc1092tx                      |
| **CPU**          | Intel Core i5-9300H (Coffee Lake-H, 45W) |
| **iGPU**         | Intel UHD Graphics 630                   |
| **dGPU**         | NVIDIA GeForce GTX 1650 *(disabled)*     |
| **RAM**          | 16 GB DDR4 @ 2666 MHz                    |
| **Storage**      | 512 GB NVMe SSD                          |
| **Wi-Fi**        | Intel Wireless-AC (Replaced with AirportItlwm) |
| **Bluetooth**    | Intel Bluetooth *(via IntelBluetoothFirmware + BlueToolFixup)* |
| **Audio**        | Realtek ALC295 (AppleALC with `alcid=3`) |
| **Display**      | 15.6” FHD (1920x1080, Internal)          |
| **Ports**        | USB-A, USB-C (DisplayPort Alt Mode)      |

---

## 🔧 OpenCore Details

| Setting         | Value                     |
|----------------|---------------------------|
| **OpenCore Version** | 1.0.4 (or latest stable supported) |
| **SMBIOS**           | MacBookPro15,2         |
| **macOS Version**    | macOS Sequoia 15.1     |
| **Boot Args**        | `debug=0x100 keepsyms=1 alcid=3 -igfxblt` |

---

## 🛠️ Easy EFI Generation – OpenCore Simplified

To simplify the EFI creation and modification process, you can use **[OpenCore Simplified](https://github.com/5T33Z0/OC-Little)**:

- A graphical tool for **generating, editing, and managing OpenCore EFI folders**.
- Great for beginners and advanced users to configure `config.plist` without errors.
- Includes built-in tools for adding/validating kexts, ACPI patches, boot-args, and more.

> 📌 Tip: Use OpenCore Simplified to quickly update this EFI to match your hardware or macOS version. Just load your existing `config.plist`, make changes, and export.


## ✅ Working Features

- ✅ Intel UHD 630 graphics with hardware acceleration
- ✅ USB ports (properly mapped with USBMap.kext)
- ✅ Internal display (EDID patched if required)
- ✅ Wi-Fi using AirportItlwm (OpenIntelWireless)
- ✅ Bluetooth (IntelBluetoothFirmware + Injector)
- ✅ Audio via AppleALC
- ✅ Battery status and sensors (VirtualSMC + SMCBatteryManager)
- ✅ Brightness control
- ✅ Sleep/Wake
- ✅ Trackpad and keyboard (via VoodooRMI and VoodooInput)
- ✅ USB-C DisplayPort output (with framebuffer patching)


## 📡 Native Wi-Fi Support (Intel + AirportItlwm)

This EFI uses `AirportItlwm.kext` to enable Wi-Fi on Intel wireless cards.  
To make **native Wi-Fi functionality** work properly on macOS Sequoia 15.1, you must use **OpenCore Legacy Patcher (OLCP)**:

- After macOS installation, run **OLCP** and apply **Post-Install Root Patches**.
- These patches are required to enable the native macOS networking stack that `AirportItlwm` relies on.
- Without OLCP patches, Wi-Fi may not function correctly or may not be detected at all.

> ⚠️ Note: While `AirportItlwm` enables Intel Wi-Fi, **features like AirDrop, Handoff, and Continuity are not supported**. For full native support, consider replacing the card with a compatible Broadcom chipset.
---

## ⚠️ Not Working / Issues

- ❌ NVIDIA GeForce GTX 1650 (macOS does not support Kepler+ NVIDIA GPUs without web drivers)
- ❌ AirDrop / Handoff *(unless using compatible Broadcom Wi-Fi card)*
- ❌ HDMI Audio (if external display via USB-C lacks audio path)
- ⚠️ Internal display may turn off/crash under certain SMBIOS — **MacBookPro15,2 is most stable so far**

---

## 📝 Notes

- **Framebuffer patches** applied to enable DisplayPort via USB-C.
- `AirportItlwm.kext` is used for Intel Wi-Fi support on Sequoia 15.1.
- Use **macOS Sequoia 15.1** specifically; newer versions may require updated kexts or patches.
- `alcid=3` used for ALC295 codec — may vary depending on layout support.
- For SMBIOS consistency, **MacBookPro15,2** was chosen due to best compatibility with this hardware.

---

## ⚠️ Disclaimer

> This EFI is tailored specifically for **HP Omen 15-dc1092tx** with the specs listed above.  
> Your mileage may vary if your hardware differs even slightly.  
> Always make sure to **generate your own SMBIOS** using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to avoid serial number duplication.

---

## 🛠️ Credits

- [Acidanthera](https://github.com/acidanthera) – OpenCore, Lilu, AppleALC, WhateverGreen, VirtualSMC, etc.
- [OpenIntelWireless](https://github.com/OpenIntelWireless) – AirportItlwm and Bluetooth kexts
- [USBMap by CorpNewt](https://github.com/corpnewt/USBMap)
- [Hackintosh Community](https://dortania.github.io/) – For the incredible documentation

---
## 🔗 License

This repository is for personal and educational purposes only. Do not distribute EFI folders with pre-generated serials.

