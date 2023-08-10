### Config Env

As the name suggests, the name of the configuration file

### Kernel Source

Change to your kernel warehouse address

For example: https://github.com/Diva-Room/Miku_kernel_xiaomi_wayne.git

> If it is a git repository, please fill in the link containing `.git`

Support direct link of git repository or zip compressed package, tar.gz compressed package

### Kernel Source Branch

Modify to your kernel branch

Example: TDA

### Kernel Config

Change to your kernel configuration file name

Example: vendor/wayne_defconfig

### Arch

Example: arm64

### Kernel Image Name

Modify it to the kernel binary that needs to be flashed, which is generally consistent with the BOARD_KERNEL_IMAGE_NAME in your aosp-device tree

Example: Image.gz-dtb

Common are Image, Image.gz

### Clang

#### Enable Clang

Due to the needs of [#75](https://github.com/xiaoleGun/KernelSU_Action/issues/75), we provide a customizable whether to enable Clang compilation

You can choose whether to enable Clang compilation

#### Use AOSP Clang

Optionally use AOSP's Clang

#### AOSP Clang Branch

Due to the needs of [#23](https://github.com/xiaoleGun/KernelSU_Action/issues/23), we provide the option to customize the Google upstream branch, the main branches are
| Clang branch |
| ---------- |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

Or other branches, please search in https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 according to your needs

#### AOSP Clang Version

Fill in the Clang version to be used
| Clang Version | Corresponding Android Version | AOSP-Clang Version |
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b |
| 14.0.6 | Android T | r450784d |
| 14.0.7 | | r450784e |
| 15.0.1 | | r458507 |

***Google's official documentation is like this, but it has been verified that individual versions cannot be downloaded***

Generally, Clang12 can pass the compilation of most 4.14 and above kernels
My own MI 6X 4.19 uses ~~r450784d~~r450784e

#### Use Custom Clang

You can use Google's official Clang, such as [ZyCromerZ-Clang](https://github.com/magojohnji/ZyCromerZ-Clang)

#### Custom Clang Source

> If it is a git repository, please fill in the link containing `.git`

Support direct link of git repository or zip compressed package, tar.gz compressed package

#### Custom Clang Branch

Forks of custom third-party Clang, e.g. `main`

### GCC

#### Enable GCC

Enable GCC cross compilation

#### Enable AOSP GCC ARM64

Download Google's official AOSP GCC and enable GCC 64 cross-compilation

#### Enable GCC ARM32

Download Google's official AOSP GCC and enable GCC 32 cross-compilation

#### AOSP GCC System

The type of system used to compile the kernel

If compiling with macOS, fill in darwin-x86

#### AOSP GCC ARM64 Version

As the name suggests, the AOSP GCC ARM64 version

#### AOSP GCC ARM32 Version

As the name suggests, the AOSP GCC ARM32 version

#### AOSP GCC Android Version

As the name suggests, the Android version corresponding to AOSP GCC

#### AOSP GCC Release

As the name implies, the Android version release version corresponding to AOSP GCC

### Enable KernelSU

Enable KernelSU, for troubleshooting kernels or compiling kernels separately

#### Kernel Installer

Link to KernelSU's install script for using third-party versions

For example: tiann original version: https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
       Modified version of MlgmXyysd: https://raw.githubusercontent.com/MlgmXyysd/KernelSU_Debug/master/kernel/setup.sh

#### KernelSU Branch or Tag

Select KernelSU branch or tag:

- main branch (development version): `KERNELSU_TAG=main`
- Latest TAG (stable version): `KERNELSU_TAG=`
- Specify TAG (such as `v0.5.2`): `KERNELSU_TAG=v0.5.2`

#### KernelSU Manager signature size and hash

Customize the size value and hash value of the KernelSU manager signature. If you do not need a custom manager, please leave it blank or fill in the official default value:

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=0xb0b91415`

You can type `ksud debug get-sign <apk_path>` to get the size value and hash value of the apk signature

### Build KernelSU Boot IMG

> Merged from the previous Workflows, you can view the historical submission

To compile boot.img containing KernelSU, you need to provide `KernelSU Source boot image`

### KernelSU Source Boot Image

As the name suggests, providing a boot image that the source system can boot normally requires a direct link, preferably the same set of kernel source code and the same set of device tree as your current system built from aosp. The ramdisk contains the partition table and init, if not, the built image will not be able to boot normally.

For example: https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot-wayne-from-Miku-UI-latest.img

### Enable Magisk

As the name suggests, configure whether to enable Magisk

### Magisk APK

As the name suggests, it provides a Magisk APK file (ZIP is also possible, theoretically as long as it is a file in ZIP format), which requires a direct link and supports third-party and custom versions of Magisk.

If you can't find the official warehouse, you can go to [magisk-files-host](https://github.com/magojohnji/magisk-files-host) to find the APK file,

It is also possible to disassemble the json to find the link.

###Magisk Patch Partition

The name of the partition patched by Magisk

Generally speaking, it is the boot partition, but it does not rule out the possibility that some devices are init_boot or vendor_boot, see Magisk official documentation for details.

### Magisk Source Boot Image

The image file of the partition patched by Magisk needs to be directly linked.

### Disable LTO

LTO is used to optimize the kernel, but sometimes it can cause errors

### Disable CC_WERROR

It is used to repair some kernels that do not support or disable Kprobes, and repair KernelSU that does not detect variables with Kprobes enabled, throwing warnings and causing errors

### Add Kprobes Config

Automatically inject parameters in defconfig

### Add overlayfs Config

This parameter provides support for KernelSU modules and system partition read and write
Automatically inject parameters in defconfig

### Enable ccache

Enable caching to make the second compilation of the kernel faster, at least 2/5 of the time can be reduced

### Need DTBO

Upload DTBO
Some devices require

### Extra cmds

Some kernels need to add some other compilation commands to compile normally. Generally, no other commands are needed. Please search for the information of your own kernel
Please separate commands with spaces

Example: LLVM=1 LLVM_IAS=1

### TC Custom cmds

Compile the toolchain configuration, you should be able to change these configurations by yourself :)