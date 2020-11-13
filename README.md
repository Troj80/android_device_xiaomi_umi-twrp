# android_device_xiaomi_umi-twrp
For building TWRP for Xiaomi Mi 10

TWRP device tree for Xiaomi Mi 10

Kernel and all blobs are extracted from MIUI 12 12.2.2 - Android 11 firmware.

The Xiaomi Mi 10 (codenamed _"umi"_) are high-end smartphone from Xiaomi.

Xiaomi Mi 10 was announced and released in February 2020.

## Device specifications

| Device       | Xiaomi Mi 10                     |
| -----------: | :------------------------------------------ |
| SoC          | Qualcomm SM8250 Snapdragon 865              |
| CPU          | 8x Qualcomm® Kryo™ 585 up to 2.84GHz        |
| GPU          | Adreno 630                                  |
| Memory       | 8GB / 12GB RAM (LPDDR5)                     |
| Shipped Android version | 10                               |
| Storage      | 128GB / 256GB / 512GB UFS 3.0 flash storage |
| Battery      | Non-removable Li-Po 4780mAh                 |
| Dimensions   | 162.58 x 74.8 x 8.96 mm                     |
| Display      | 2340 x 1080 (19.5:9), 6.67 inch             |

## Device picture

![Xiaomi Mi 10](https://cdn.cnbj0.fds.api.mi-img.com/b2c-shopapi-pms/pms_1581494372.61732687.jpg)

## Features

**Works**
```
- Booting
- USB-OTG
- ADB
- MTP
- Super partition functions(Dynamic partition)
```
**Not Working**
```
- [Decryption](https://github.com/simonsmh/android_bootable_recovery/commits/android-10.0)(not supported by Android 11)
```
## Compile
```
sudo apt update&&sudo apt install git-core gnupg flex bison gperf zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache 
libgl1-mesa-dev libxml2-utils xsltproc unzip openjdk-8-jdk build-essential git repo fastboot adb
```
## Configuration ccache:
```
# Enable ccache
export USE_CCACHE=1
# Change ccache path
export CCACHE_DIR=~/.ccache
# Take effect
source ~/.bashrc
# Configure ccache size
ccache -M 50G
```
## Create Twrp folder
```
mkdir -p twrp&&cd twrp
```
## Synchronize Twrp's omni minimum Tree:
```
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_omni.git -b twrp-10.0
repo sync -j8
```
## Add this item to .repo/manifest.xml:
```
<project path="device/xiaomi/umi" name="Troj80/android_device_xiaomi_umi-twrp" remote="github" revision="android-11.0" />
```
## Synchronize Device Tree:
```
repo sync --force-sync device/xiaomi/umi
```
## Start compiling:
```
. build/envsetup.sh
lunch omni_umi-eng
mka recoveryimage ALLOW_MISSING_DEPENDENCIES=true # Only if you use minimal twrp tree.
```
## TWRP test:
```
fastboot boot out/target/product/umi/recovery.img
```
## Flash TWRP:
```
fastboot flash recovery out/target/product/umi/recovery.img
```
