### Config Env

顾名思义，配置文件的名称

### Kernel Source

修改为你的内核仓库地址

例如: https://github.com/Diva-Room/Miku_kernel_xiaomi_wayne.git

> 如果是 git 仓库，请填写包含`.git`的链接

支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

### Kernel Source Branch

修改为你的内核分支

例如: TDA

### Kernel Config

修改为你的内核配置文件名

例如: vendor/wayne_defconfig

### Arch

例如: arm64

### Kernel Image Name

修改为需要刷写的 kernel binary，一般与你的 aosp-device tree 里的 BOARD_KERNEL_IMAGE_NAME 是一致的

例如: Image.gz-dtb

常见还有 Image、Image.gz

### Clang

#### Enable Clang

由于 [#75](https://github.com/xiaoleGun/KernelSU_Action/issues/75) 的需要，我们提供可自定义 是否开启 Clang 编译

可以选择是否开启 Clang 编译

#### Use AOSP Clang

可以选择是否用 AOSP 的 Clang

#### AOSP Clang Branch

由于 [#23](https://github.com/xiaoleGun/KernelSU_Action/issues/23) 的需要，我们提供可自定义 Google 上游分支的选项，主要的有分支有
| Clang 分支 |
| ---------- |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

或者其它分支，请根据自己的需求在 https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 中寻找

#### AOSP Clang Version

填写需要使用的 Clang 版本
| Clang 版本 | 对应 Android 版本 | AOSP-Clang 版本 |
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b |
| 14.0.6 | Android T | r450784d |
| 14.0.7 | | r450784e |
| 15.0.1 | | r458507 |

***谷歌官方文档如此，但经验证个别版本无法下载***

一般 Clang12 就能通过大部分 4.14 及以上的内核的编译
我自己的 MI 6X 4.19 使用的是 ~~r450784d~~ r450784e

#### Use Custom Clang

可以使用除 Google 官方的 Clang，如[ZyCromerZ-Clang](https://github.com/magojohnji/ZyCromerZ-Clang)

#### Custom Clang Source

> 如果是 git 仓库，请填写包含`.git`的链接

支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

#### Custom Clang Branch

自定义第三方 Clang 的分支，例如 `main`

### GCC

#### Enable GCC 

启用 GCC 交叉编译

#### Enable AOSP GCC ARM64

下载 Google 官方的 AOSP GCC，启用 GCC 64 交叉编译

#### Enable GCC ARM32

下载 Google 官方的 AOSP GCC，启用 GCC 32 交叉编译

#### AOSP GCC System

用于编译内核的系统类型

如果使用 macOS 编译，则填写 darwin-x86

#### AOSP GCC ARM64 Version

顾名思义，AOSP GCC ARM64 的版本

#### AOSP GCC ARM32 Version

顾名思义，AOSP GCC ARM32 的版本

#### AOSP GCC Android Version

顾名思义，AOSP GCC 所对应的 Android 的版本

#### AOSP GCC Release

顾名思义，AOSP GCC 所对应的 Android 的版本发布版本

### Enable KernelSU

启用 KernelSU，用于排查内核故障或单独编译内核

#### Kernel Installer

KernelSU 的安装脚本链接，以便使用第三方版本

例如：tiann 原版：https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
      MlgmXyysd修改版：https://raw.githubusercontent.com/MlgmXyysd/KernelSU_Debug/master/kernel/setup.sh

#### KernelSU Branch or Tag

选择 KernelSU 的分支或 tag:

- main 分支(开发版): `KERNELSU_TAG=main`
- 最新 TAG(稳定版): `KERNELSU_TAG=`
- 指定 TAG(如`v0.5.2`): `KERNELSU_TAG=v0.5.2`

#### KernelSU Manager signature size and hash

自定义KernelSU管理器签名的size值和hash值，如果不需要自定义管理器则请留空或填入官方默认值：

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=0xb0b91415`

可键入`ksud debug get-sign <apk_path>`获取apk签名的size值和hash值

### Build KernelSU Boot IMG

> 从之前的 Workflows 合并进来的，可以查看历史提交

编译含KernelSU的 boot.img，需要你提供`KernelSU Source boot image`

### KernelSU Source Boot Image

故名思义，提供一个源系统可以正常开机的 boot 镜像，需要直链，最好是同一套内核源码以及与你当前系统同一套设备树从 aosp 构建出来的。ramdisk 里面包含分区表以及 init，没有的话构建出来的镜像会无法正常引导。

例如: https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot-wayne-from-Miku-UI-latest.img

### Enable Magisk

顾名思义，配置是否启用 Magisk

### Magisk APK

故名思义，提供一个 Magisk APK 文件（ZIP也可以，理论上只要是ZIP格式的文件就可以了），需要直链，支持第三方、自定义版本的 Magisk。

如果找不到官方仓库，可以去 [magisk-files-host](https://github.com/magojohnji/magisk-files-host) 找APK文件，

拆json找链接也可以。

### Magisk Patch Partition

Magisk 所修补的分区名称

一般来说，是boot分区，但不排除部分设备是 init_boot 或 vendor_boot 的可能性，详见 Magisk 官方文档。

### Magisk Source Boot Image

Magisk 所修补的分区的镜像文件，需要直链。

### Disable LTO

LTO 用于优化内核，但有些时候会导致错误

### Disable CC_WERROR

用于修复某些不支持或关闭了Kprobes的内核，修复KernelSU未检测到开启Kprobes的变量抛出警告导致错误

### Add Kprobes Config

自动在 defconfig 注入参数

### Add overlayfs Config

此参数为 KernelSU 模块和 system 分区读写提供支持
自动在 defconfig 注入参数

### Enable ccache

启用缓存，让第二次编译内核更快，最少可以减少 2/5 的时间

### Need DTBO

上传 DTBO
部分设备需要

### Extra cmds

有的内核需要加入一些其它编译命令，才能正常编译，一般不需要其它的命令，请自行搜索自己内核的资料
请在命令与命令之间用空格隔开

例如: LLVM=1 LLVM_IAS=1

### TC Custom cmds

编译工具链配置，自己改改这些配置应该都会吧 :)