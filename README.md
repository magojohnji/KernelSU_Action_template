[Chinese (Simplified)](README_ZH-HANS.md) | **English**

# KernelSU_Action

## :warning: :warning: :warning: **Read README frist !!!!!**

The ***Plus*** version, can compile kernel, AnyKernel3 and boot image

The Actions to compile the Non-GKI kernel, with the optional addition of Magisk and KernelSU, is somewhat universal.

:warning: **The essence of this project is to simplify the configuration of the compilation environment and other steps (all similar repositories are), the kernel compilation of the parameters still need to find your own, otherwise the compilation will fail!**

## ***Tested Kernels***

- *`5.15`*
- *`5.10`*
- *`5.4`*
- *`4.19`*
- *`4.14`*
- *`4.9`*
- *`4.4`*
- *The other versions* ***may*** *be supported, but you need to try it for yourself!*

## **Usage**

:warning: :warning: :warning: `After compilation, AnyKernel3 will be uploaded in `Action` and so on, device checking has been turned off, please make sure your phone is unlocked before flashing it!`

- Star this repository and click "Use this template" to create the repository the way you want it.

`Star is a source of motivation for authors, so please don't skimp on your Star!`

- Rename the configuration file to `config.properties` (the name can be customized, as long as it is a plain text file)

- Write your favorite configuration in the configuration file, whose comments can be found in the lower part of this README.md.

- Open the workflow file (name is customizable, default is [build-kernel.yml] (.github/workflows/build-kernel.yml)) and find the following:


```yaml
    steps.
    - name: Check out
      uses: actions/checkout@v3

    - name: Read Building Configuration
      run: |


->>>>>>> CONFIG_ENV=config.properties.example <<<<<<<-


        echo "KERNEL_SOURCE=$(cat $CONFIG_ENV | grep -w "KERNEL_SOURCE" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
        echo "KERNEL_SOURCE_BRANCH=$(cat $CONFIG_ENV | grep -w "KERNEL_SOURCE_BRANCH" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
        echo "KERNEL_CONFIG=$(cat $CONFIG_ENV | grep -w "KERNEL_CONFIG" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
```

- Change **`config.properties.example`** to the name of your configuration file. If you created a config file called **`config_abcdefg.envaaa`** then you should fill in **`config_abcdefg.envaaa`** here.

- After that go to Actions and click on the green button `I understand my workflows, go ahead and enable them.` Click on Options (default is **`Build`**) and you'll see **`Run workflows`** at the top of the big dialog on the right, clicking on that will start the build. If **`Release`** is checked, it will release the build.

## ***Warning!*** :warning: :warning: :warning:

Please **be sure** to first **carefully, conscientiously** read and **understand** the following config file comments!!!

**Otherwise you'll get the wrong product, or Actions won't work at all!**

<details>
  <summary><h3>❓How to write a configuration❓ <h3></summary>

## ***Configuration***

**Some of these configurations contradict each other, please figure out the logic before configuring!!!!**

---

### **Kernel**

---
 
#### Kernel Source

(HTTP link)

Change to your kernel repository address

Example: https://github.com/magojohnji/msm-4.14.git

Support direct links to git repositories or zip or tar.gz archives.

> Tips: git repositories are preferred.

#### Kernel Source Branch

(string)

Change this to the name of your kernel branch

e.g. TDA, base, su, 13, R. Check it out!

#### Kernel Config

(string)

Modify this to the name of your kernel configuration file

e.g. vendor/wayne_defconfig, vendor/violet-perf_defconfig, munch_defconfig etc.

> Tips: Look in arch/arm64/configs(/vendor) in the kernel source.

#### Arch

(string)

Change it to your CPU architecture, usually arm64.

Example: arm64

#### Kernel Image Name

(string)

Modify it to the kernel binary to be flashed, usually the same as BOARD_KERNEL_IMAGE_NAME in your aosp-device tree.

Example: Image.gz-dtb

Other common ones are Image, Image.gz.

### **Clang**

---

#### Enable Clang

(true or false)

We provide a customizable way to enable or disable Clang compilation


#### Use AOSP Clang

(true or false)

You can choose whether to use AOSP Clang or not.

#### AOSP CLANG System

(String)

The system to which Clang applies

Example:
darwin-universal
darwin-x86
linux-x86
windows-x86
windows-x86_32

Default is `linux-x86`, please go to [AOSP Clang](https://android.googlesource.com/platform/prebuilts/clang/host/) for customization.

#### AOSP Clang Branch

(String)

We provide the option to customize Google's upstream branches, the main ones being

| Clang Branch
| ---------- |
| main |
| master |
| master-kernel-build-2021 | master-kernel-build-2021 | master-kernel-build-2021
| master-kernel-build-2022 | master-kernel-build-2022 | master-kernel-build-2022

Or any other branch, look for it at https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 if you need it.

#### AOSP Clang Version

(string)

Fill in the Clang version you want to use
| Clang Version | Android Version | AOSP-Clang Version |  |  | AOSP-Clang Version | AOSP Clang Version
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b | 14.0.6 | Android S | r416183b | Android S
| 14.0.6 | Android T | r450784d | 14.0.7 | Android T | r450784b
| 14.0.7 | r450784e | 15.0.1 | r416183b
| 15.0.1 | | r458507 |

***Official Google docs are like this, but it's been verified that individual versions can't be downloaded, so if you can't download it, please set it to r450784e***.

Generally, Clang12 can be compiled with most kernels from 4.14 and up.
My own Redmi Note 7 Pro (Kenrel 4.14) uses ~~r450784d~~ r450784e

> Tips: If you still get an error, go to [AOSP Clang](https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86) and look for available branches and versions.

#### Use Custom Clang

(true or false)

You can use other clangs than Google's official one, e.g. [ZyCromerZ-Clang](https://github.com/magojohnji/ZyCromerZ-Clang).

#### Custom Clang Source

(HTTP link)

Supports direct links to git repositories or zip or tar.gz archives.

> Tips: If it is a git repository, please fill in the link with `.git`.

#### Custom Clang Branch

(string)

If you are using a custom Clang, you can customize the branch of a third-party Clang, e.g. ``main``.

### **GCC**

---

#### Enable GCC 

(true or false)

Configurable to enable GCC cross-compilation

#### Enable AOSP GCC ARM64

(true or false)

Whether or not to download the official Google AOSP GCC and enable GCC 64 cross-compilation

If **`Enable GCC `** is set to false, then this item is meaningless.

#### Enable GCC ARM32

(true or false)

Whether or not to download Google's official AOSP GCC and enable GCC 32 cross compilation

This item is meaningless if **`Enable GCC `** is set to false.

#### AOSP GCC System

(string)

The type of system used to compile the kernel

> Tips: if compiling with macOS, enter darwin-x86

#### AOSP GCC ARM64 Version

(string)

As the name suggests, the version number of AOSP GCC ARM64, usually defaults to `aarch64-linux-android-4.9`.

#### AOSP GCC ARM32 Version

(string)

As the name suggests, the version of AOSP GCC ARM32, usually defaults to `arm-linux-androideabi-4.9`.

#### AOSP GCC Android Version

(String)

As the name suggests, the version of Android that AOSP GCC corresponds to.

e.g. 12.1.0, 10.0.0.

#### AOSP GCC Release

(String)

As the name suggests, it is the version number of the AOSP GCC release.

e.g. r27

> Tips: If you want to customize the above AOSP GCC, please go to [AOSP Gcc] (if you want to customize it, please go to https://android.googlesource.com/platform/prebuilts/gcc/) to find the available branches and versions.

#### Use Custom Gcc 64

(true or false)

You can configure whether to use custom Gcc 64 or not.

This item is meaningless if **`Enable GCC`** is set to false.

#### Custom Gcc 64 Source

(HTTP link)

Custom Gcc 64 source code, support git repositories or direct links to zip or tar.gz archives.

> Tips: If it is a git repository, please fill in the link with `.git`.

#### Custom Gcc 64 Branch

(string)

If you use Custom Gcc 64, you can customize the branch of a third-party Gcc, e.g. `main`.

#### Custom Gcc 64 Bin

(String)

Customize the name of the Gcc 64 executable, AOSP Gcc is `aarch64-linux-android-`.

#### Use Custom Gcc 32

(true or false)

You can configure whether to use custom Gcc 32

If **`Enable GCC `** is set to false, then this item is meaningless.

#### Custom Gcc 32 Source

(HTTP link)

Custom Gcc 32 source code, support git repositories or direct links to zip or tar.gz archives.

> Tips: If it is a git repository, please fill in the link with `.git`.

#### Custom Gcc 32 Branch

(string)

If you use custom Gcc 32, you can customize the branch of a third-party Gcc, e.g. ``main``.

#### Custom Gcc 32 Bin

(String)

Customize the name of the Gcc 32 executable, for AOSP Gcc it is `arm-linux-androideabi-`.


### **Enable KernelSU**

(true or false)

Enable KernelSU for troubleshooting the kernel or compiling the kernel separately.

#### Kernel Installer

(HTTP link)

Link to the KernelSU installer script to use third-party versions.

> Tips:
tiann Original: https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
MlgmXyysd modified version: https://raw.githubusercontent.com/MlgmXyysd/KernelSU_Debug/master/kernel/setup.sh

#### KernelSU Branch or Tag

(String)

Select a branch or tag for KernelSU: main branch (development version).

- `main` branch (development version): `KERNELSU_TAG=main`
- Newest TAG (stable): `KERNELSU_TAG=`
- Specified TAG (e.g., `v0.5.2`): `KERNELSU_TAG=v0.5.2`.

Please find your own

#### KernelSU Manager signature size and hash

(string)

Customize the KernelSU manager signature size and hash value, if you don't need to customize the manager, please leave it empty or fill in the official default value:

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=0xb0b91415`.

You can type `ksud debug get-sign <apk_path>` to get the size and hash of the apk signature.

#### Build KernelSU Boot IMG

(true or false)

> Merged in from previous Workflows, you can see the commit history

Build boot.img with KernelSU, you need to provide `KernelSU Source boot image`.

#### KernelSU Source Boot Image

(HTTP link)

As the name suggests, you need to provide a boot image of the source system that can boot normally, it needs to be a direct link, preferably built from aosp with the same kernel source code and the same device tree as your current system. ramdisk contains the partition table and init, without it, the built image will not boot normally.

Example: https://raw.githubusercontent.com/abc/def/main/boot/boot.img

### **Build Settings**

---

#### Disable LTO

(true or false)

LTO is used to optimize the kernel, but in some cases it can cause errors

#### Disable CC_WERROR

(true or false)

Used to fix some kernels that don't support or disable Kprobes, fixes KernelSU not detecting Kprobes-enabled variables throwing warnings and causing errors.

#### Add Kprobes Config

(true or false)

Automatically inject parameters into defconfig to enable Kprobes support.

#### Add overlayfs Config

(true or false)

Provide support for reading and writing to KernelSU modules and system partitions, automatically injected in defconfig.

#### Enable ccache

(true or false)

Enable caching to make the second kernel build faster, at least 2/5 of the time.

#### Need DTBO

(true or false)

Upload DTBO
Required for some devices

#### Extra cmds

(strings)

Some kernels need to add some other compilation commands to compile properly, usually no other commands are needed, please search your own kernel's information.
Please use space between commands.

Example: LLVM=1 LLVM_IAS=1

#### TC Custom cmds

(strings)

Compile toolchain configuration, ~~ you should be able to change these configurations yourself :)~~ Ask the kernel author or analyze the kernel compilation scripts yourself.


## ***Useful tips*** (congratulations on reading through the ***`configuration`*** part)

- If you want to build automatically after modifying the file, you can change the beginning of [build-kernel.yml](.github/workflows/build-kernel.yml) to this:

```yaml
name: Build
on.
  Build on.
    branches: [ main ]
  workflow_dispatch.
    workflow_dispatch: workflow_dispatch: workflow_dispatch.
      release.
        description: "Release"
        required: true
        default: false
        type: boolean

```

- If you want a daily timed build, you can change the beginning of [build-kernel.yml](.github/workflows/build-kernel.yml) to look like this: (executed daily at 2:00 UTC)

```yaml
name: Build
on.
  schedule.
    - cron: "0 2 * * * *"
  workflow_dispatch.
    cron: "0 * * *" workflow_dispatch.
      cron: "0 * * *" workflow_dispatch: inputs.
        description: "Release"
        required: true
        default: false
        type: boolean
```

Of course you can mix them up :-)

</details>

<details>
  <summary><h3>config.properties instance<h3></summary>

## File
This file is for compiling RMX1971 Kernel 4.9 (Realme Q) with KernelSU:

```properties
KERNEL_SOURCE=https://gitlab.com/kssrao13882/kernel_realme_sdm710.git
KERNEL_SOURCE_BRANCH=13
KERNEL_CONFIG=KharaMe_defconfig
KERNEL_IMAGE_NAME=Image.gz
ARCH=arm64

ENABLE_CLANG=true
USE_AOSP_CLANG=false
AOSP_CLANG_SYSTEM=
AOSP_CLANG_BRANCH=
AOSP_CLANG_VERSION=
USE_CUSTOM_CLANG=true
CUSTOM_CLANG_SOURCE=https://github.com/kdrag0n/proton-clang.git
CUSTOM_CLANG_BRANCH=master

ENABLE_GCC=true
ENABLE_AOSP_GCC_ARM64=true
ENABLE_AOSP_GCC_ARM32=true
AOSP_GCC_SYSTEM=linux-x86
AOSP_GCC_ARM64_VERSION=aarch64-linux-android-4.9
AOSP_GCC_ARM32_VERSION=arm-linux-androideabi-4.9
AOSP_GCC_ANDROID_VERSION=12.1.0
AOSP_GCC_RELEASE=r27
USE_CUSTOM_GCC_64=false
CUSTOM_GCC_64_SOURCE=
CUSTOM_GCC_64_BRANCH=
CUSTOM_GCC_64_BIN=aarch64-linux-android-
USE_CUSTOM_GCC_32=false
CUSTOM_GCC_32_SOURCE=
CUSTOM_GCC_32_BRANCH=
CUSTOM_GCC_32_BIN=arm-linux-androideabi-

ENABLE_KERNELSU=true
KERNELSU_INSTALLER=https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
KERNELSU_TAG=main
KSU_EXPECTED_SIZE=
KSU_EXPECTED_HASH=
BUILD_KERNELSU_BOOT_IMG=true
KERNELSU_SOURCE_BOOT_IMAGE=https://raw.githubusercontent.com/magojohnji/MAKSU/main/boot/boot_PE13_rmx1971.img

DISABLE-LTO=false
DISABLE_CC_WERROR=false
ADD_KPROBES_CONFIG=true
ADD_OVERLAYFS_CONFIG=true
ENABLE_CCACHE=true
NEED_DTBO=false
BUILDER_HOST=Github-Action

TC_CUSTOM_CMDS:CLANG_TRIPLE=aarch64-linux-gnu- CROSS_COMPILE=aarch64-linux-androidkernel-
EXTRA_CMDS:

```

This file is for compiling violet Kernel 4.14 (Redmi Note 7 Pro) with KernelSU:

```properties
KERNEL_SOURCE=https://github.com/magojohnji/msm-4.14.git
KERNEL_SOURCE_BRANCH=R
KERNEL_CONFIG=vendor/violet-perf_defconfig
KERNEL_IMAGE_NAME=Image.gz-dtb
ARCH=arm64

ENABLE_CLANG=true
USE_AOSP_CLANG=false
AOSP_CLANG_SYSTEM=
AOSP_CLANG_BRANCH=
AOSP_CLANG_VERSION=
USE_CUSTOM_CLANG=true
CUSTOM_CLANG_SOURCE=https://gitlab.com/Panchajanya1999/azure-clang.git
CUSTOM_CLANG_BRANCH=main

ENABLE_GCC=true
ENABLE_AOSP_GCC_ARM64=false
ENABLE_AOSP_GCC_ARM32=false
AOSP_GCC_SYSTEM=
AOSP_GCC_ARM64_VERSION=
AOSP_GCC_ARM32_VERSION=
AOSP_GCC_ANDROID_VERSION=
AOSP_GCC_RELEASE=
USE_CUSTOM_GCC_64=true
CUSTOM_GCC_64_SOURCE=https://github.com/magojohnji/gcc-arm64.git
CUSTOM_GCC_64_BRANCH=gcc-master
CUSTOM_GCC_64_BIN=aarch64-linux-android-
USE_CUSTOM_GCC_32=true
CUSTOM_GCC_32_SOURCE=https://github.com/magojohnji/gcc-arm32.git
CUSTOM_GCC_32_BRANCH=master
CUSTOM_GCC_32_BIN=arm-linux-androideabi-

ENABLE_KERNELSU=true
KERNELSU_INSTALLER=https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
KERNELSU_TAG=main
KSU_EXPECTED_SIZE=
KSU_EXPECTED_HASH=
BUILD_KERNELSU_BOOT_IMG=true
KERNELSU_SOURCE_BOOT_IMAGE=https://raw.githubusercontent.com/magojohnji/bin/main/boot_PE13_violet.img

DISABLE-LTO=false
DISABLE_CC_WERROR=false
ADD_KPROBES_CONFIG=true
ADD_OVERLAYFS_CONFIG=true
ENABLE_CCACHE=true
NEED_DTBO=false
BUILDER_HOST=Github-Action

TC_CUSTOM_CMDS:CROSS_COMPILE=aarch64-linux-gnu- CROSS_COMPILE_ARM32=arm-linux-gnueabi-
EXTRA_CMDS:AR=llvm-ar OBJDUMP=llvm-objdump STRIP=llvm-strip NM=llvm-nm OBJCOPY=llvm-objcopy LD=ld.lld

```
This file is for compiling munch Kernel 4.19 (Redmi K40S) with KernelSU:

```properties
KERNEL_SOURCE=https://github.com/magojohnji/Realking_kernel_sm8250.git
KERNEL_SOURCE_BRANCH=base
KERNEL_CONFIG=munch_defconfig
KERNEL_IMAGE_NAME=Image.gz
ARCH=arm64

ENABLE_CLANG=true
USE_AOSP_CLANG=false
AOSP_CLANG_SYSTEM=
AOSP_CLANG_BRANCH=
AOSP_CLANG_VERSION=
USE_CUSTOM_CLANG=true
CUSTOM_CLANG_SOURCE=https://github.com/ZyCromerZ/Clang/releases/download/18.0.0-20230901-release/Clang-18.0.0-20230901.tar.gz
CUSTOM_CLANG_BRANCH=

ENABLE_GCC=false
ENABLE_AOSP_GCC_ARM64=false
ENABLE_AOSP_GCC_ARM32=false
AOSP_GCC_SYSTEM=
AOSP_GCC_ARM64_VERSION=
AOSP_GCC_ARM32_VERSION=
AOSP_GCC_ANDROID_VERSION=
AOSP_GCC_RELEASE=
USE_CUSTOM_GCC_64=false
CUSTOM_GCC_64_SOURCE=
CUSTOM_GCC_64_BRANCH=
CUSTOM_GCC_64_BIN=aarch64-linux-android-
USE_CUSTOM_GCC_32=false
CUSTOM_GCC_32_SOURCE=
CUSTOM_GCC_32_BRANCH=
CUSTOM_GCC_32_BIN=arm-linux-androideabi-

ENABLE_KERNELSU=true
KERNELSU_INSTALLER=https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
KERNELSU_TAG=main
KSU_EXPECTED_SIZE=
KSU_EXPECTED_HASH=
BUILD_KERNELSU_BOOT_IMG=false
KERNELSU_SOURCE_BOOT_IMAGE=

MIX_KERNELSU_MAGISK_BOOT_IMAGE=false

DISABLE-LTO=false
DISABLE_CC_WERROR=false
ADD_KPROBES_CONFIG=true
ADD_OVERLAYFS_CONFIG=true
ENABLE_CCACHE=true
NEED_DTBO=true
BUILDER_HOST=Github-Action

TC_CUSTOM_CMDS:CROSS_COMPILE=aarch64-linux-gnu-
EXTRA_CMDS:NM=llvm-nm OBJDUMP=llvm-objdump STRIP=llvm-strip

```
</details>

## ***Other***

If you find something that doesn’t work, or you need to add or modify functions, please raise **[Issue](https://github.com/magojohnji/KernelSU_Action_template/issues)** to let me know!

## ***Grateful***

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [tiann](https://github.com/tiann)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)

## ***LICENSE***

    MIT License

    Copyright (c) 2023 v阿布Abu

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.