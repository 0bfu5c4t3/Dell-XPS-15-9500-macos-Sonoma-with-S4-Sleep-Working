# OpenCore EFI – Dell XPS 15 9500 (Comet Lake)

![XPS9500 Screenshot](https://github.com/user-attachments/assets/325c1f4d-6df3-4e3f-8eb5-3f66e4b5debb)

## Overview
OpenCore EFI for macOS **Sonoma 14** and **Sequoia 15** on the **Dell XPS 15 9500** with i7-10750H. Clean, stable, and ready for daily use.

---

## ✅ Hardware Compatibility

| Component        | Spec                                | Status       |
|------------------|--------------------------------------|--------------|
| **CPU**          | Intel Core i7-10750H                 | ✅ Working    |
| **iGPU**         | Intel UHD 630                        | ✅ Working    |
| **dGPU**         | NVIDIA GTX 1650Ti                    | ❌ Disabled   |
| **RAM**          | 32GB DDR4                            | ✅ Working    |
| **Display**      | 1920×1200 FHD                        | ✅ Working    |
| **Wi-Fi**        | Intel AX201 (Killer 1650s)           | ✅ Working    |
| **Bluetooth**    | AX201                                | ✅ Working    |
| **Audio**        | Realtek ALC3281                      | ✅ Working    |
| **Trackpad**     | I2C Precision Touchpad               | ✅ Working    |
| **Webcam**       | Microdia RGB IR                      | ✅ Working    |
| **MicroSD**      | RTS5260 Reader                       | ✅ Working    |
| **Fingerprint**  | Goodix Sensor                        | ❌ Not Working |
| **Sleep (S4)**   | Hibernate/Wake                       | ✅ Working    |
| **Keyboard**     | Internal QWERTY                      | ✅ Working    |
| **SSD**          | WD Black SN770                       | ✅ Working    |

---

## 🔧 BIOS Setup

Set these values in BIOS:

| Setting                  | Value       |
|--------------------------|-------------|
| SATA Operation           | AHCI        |
| Secure Boot              | Disabled    |
| Intel SGX                | Disabled    |
| SMM Security Migration   | Disabled    |
| Computrace               | Disabled    |
| VT-d                     | Disabled    |

### Mod BIOS (Undervolt support, CFG Lock)

Use [grub_setup_var](https://github.com/XDleader555/grub_setup_var/releases) or follow [this guide](https://linustechtips.com/topic/1323151-dell-xps-9700-undervolting-the-complete-guide/):

```bash
setup_var PchSetup 0x16 0x00   # Disable RTC Memory Lock  
setup_var CpuSetup 0x3E  0x00  # Disable CFG Lock  
setup_var CpuSetup 0xDA 0x00   # Disable Overclocking Lock  
```

---

## 🚀 Usage

1. Clone this repo  
2. Copy `EFI` folder to your USB's EFI partition  
3. Boot from USB  
4. Move EFI to internal drive after testing  

---

## 🔧 Post-Install Fixes

### ✅ Fix Sleep
```bash
sudo pmset -a hibernatemode 25
sudo pmset -a standby 1
sudo pmset -a powernap 1
sudo pmset -a sleep 1
sudo pmset -a standbydelaylow 1
sudo pmset -a standbydelayhigh 1
sudo pmset -a womp 0
sudo pmset -a proximitywake 0
```

> **Note:** When resuming from hibernate, macOS may show a false-positive error message. Just ignore it — it doesn’t affect functionality. Also, bluetooth is semi-broken on Sequoia.

### ✅ Utilities
- **Wi-Fi Control** – [HeliPort](https://github.com/OpenIntelWireless/HeliPort)
- **Fix Bluetooth After Sleep** – [BlueSnooze](https://github.com/odlp/bluesnooze)
- **Undervolt Tool** – [VoltageShift](https://github.com/sicreative/VoltageShift)

```bash
sudo ./voltageshift buildlaunchd -100 -60 -95 0 0 1 45 90 1 160
```

---

## 🖥 SMBIOS & Config

| Item         | Value               |
|--------------|---------------------|
| **SMBIOS**   | MacBookPro16,3      |
| **macOS**    | Sonoma 14 / Sequoia 15 |
