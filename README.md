# OpenCore EFI for Dell XPS 15 9500 (Comet Lake)
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/325c1f4d-6df3-4e3f-8eb5-3f66e4b5debb" />

# Specs
| Component | Specs |
| --------- | ----- |
| **Model** | Dell XPS 9500 |
| **SMBIOS** | MacBookPro16,3 |
| **macOS** | Sonoma (14), Sequoia (15) |
| **CPU** | Intel Core i7-10750H |
| **iGPU** | Intel UHD Graphics 630 |
| **dGPU** | NVIDIA GeForce GTX 1650Ti Mobile |
| **SSD** | WD Black SN770 |
| **Display** | 1920x1200 |
| **Wi-Fi** | Intel Killer AX1650s |
| **Touchpad** | I2C Touchpad |
| **Soundcard** | Realtek ALC3281/ALC289 |
| **Fingerprint** | Shenzhen Goodix |

# Hardware Specifications

| Hardware | Specification | Status |
| --- | --- | --- |
| CPU | Intel Core i7-10750H | ✅ Working |
| RAM | DDR4 32GB | ✅ Working |
| Audio | Realtek ALC3281 | ✅ Working |
| WiFi | Killer 1675 (AX201) | ✅ Working |
| Bluetooth | AX201 Wi-Fi 5 | ✅ Working |
| SSD | WD Black SN770 1TB | ✅ Working |
| Keyboard | - | ✅ Working |
| Trackpad | I2C Connection | ✅ Working |
| Webcam | Microdia RGB IR HD camera | ✅ Working |
| MicroSD Card | RTS5260 Card Reader | ✅ Working |
| Fingerprint Sensor | Shenzen Goodix | ❌ Not Working |
| S4 SLeep | Hibernate/Wake | ✅ Working |
| GPU | Intel HD630 Graphics | ✅ Working |
| eGPU | NVIDIA GeForce GTX 1650Ti Mobile | ❌ Not Working |
| Display | 1920 x 1200 FHD LCD | ✅ Working |

# How to use?
- Setup BIOS:

| Setting | Option |
| ------- | ------ |
| SATA Operation | AHCI |
| Secure Boot | Disabled |
| Intel SGX | Disabled |
| SMM Security Migration | Disabled |
| Absolute/Computrace | Disabled |
| VT-d/VT for direct I/O | Disabled |

- Mod BIOS using [grub shell](https://github.com/XDleader555/grub_setup_var/releases) / [How to do](https://linustechtips.com/topic/1323151-dell-xps-9700-undervolting-the-complete-guide/)
```
setup_var PchSetup 0x16 0x00 # Disable RTC Memory Lock
setup_var CpuSetup 0x3E 0x00 # Disable CFG Lock
setup_var CpuSetup 0xDA 0x00 # Disable Overclocking Lock
```
- Clone this repo
- Copy EFI folder to your USB/EFI partition
- [Follow this guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) to generate SMBIOS and fix iServices
- Use these commands to fix sleep
```
sudo pmset -a hibernatemode 25
sudo pmset -a standby 1
sudo pmset -a powernap 1
sudo pmset -a sleep 1
sudo pmset -a standbydelaylow 1
sudo pmset -a standbydelayhigh 1
sudo pmset -a womp 0
sudo pmset -a proximitywake 0
```
- Install [HeliPort](https://github.com/OpenIntelWireless/HeliPort) to control Wi-Fi
- Install [BlueSnooze](https://github.com/odlp/bluesnooze) to fix Bluetooth not working after sleep
- Undervolt with [VoltageShift](https://github.com/sicreative/VoltageShift)
```
sudo ./voltageshift buildlaunchd -100 -60 -95 0 0 1 45 90 1 160
```
