**中文（简体）** | [English](README.md)

# *Add KernelSU and Magisk Action*

## :warning: :warning: :warning: **先阅读 README！！！**

***Plus***版本，可以编译内核、AnyKernel3、boot-kernelsu.img、boot-magisk.img、magisk.zip

编译 Non-GKI 内核 的 Action，可选添加 Magisk 和 KernelSU，具有一定的普遍性。

**本仓库真实有效，如需查看编译实例可去查看本仓库的 `build` 分支。**

## ***支持的内核版本***

- *`5.4`*
- *`4.19`*
- *`4.14`*
- *`4.9`*
- ***其他版本可能支持，但是你必须自行测试！***

## ***使用***

> :warning: :warning: :warning: 编译成功后，会在 `Action` 上传 AnyKernel3 等一系列内容，已经关闭设备检查，请确保手机已经解锁后再刷入！

- Star 本仓库，然后 Fork 本仓库，以确保工作流运行正常。

> Star 是作者的动力来源，请不要吝啬你的 Star！

- 将配置文件改名为config.env（名称可以自定义，但**必须**以 `.env` 结尾 ！）

- 在配置文件中编写你喜欢的配置，配置文件的注释可以在本README.md的下半部分找到。

- 打开工作流文件（名称可自定义，默认为 [build-kernel.yml](.github/workflows/build-kernel.yml) ），找到以下内容：

```yaml
    steps:
    - name: Check out
      uses: actions/checkout@v3

    - name: Read Building Configuration
      run: |


->>>>>>> CONFIG_ENV=config.env.simple <<<<<<<-


        echo "KERNEL_SOURCE=$(cat $CONFIG_ENV | grep -w "KERNEL_SOURCE" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
        echo "KERNEL_SOURCE_BRANCH=$(cat $CONFIG_ENV | grep -w "KERNEL_SOURCE_BRANCH" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
        echo "KERNEL_CONFIG=$(cat $CONFIG_ENV | grep -w "KERNEL_CONFIG" | head -n 1 | cut -d "=" -f 2)" >> $GITHUB_ENV
```

将 **`config.env.simple`** 改为你的配置文件名称；

如果你创建了一个叫 **`config_abcdefg.env`** 的配置文件，那你就应该在这里填写 **`config_abcdefg.env`**。

- 之后进入 Actions，点击绿色按钮`I understand my workflows, go ahead and enable them.` 点击选项（默认为 `Build` ）会看见右边的大对话框的上面会有`Run workflows`，点击它会启动构建。若勾选 Release，则会发布 Release。

## ***警告*** :warning: :warning: :warning:

请**务必**先**仔细，认真**阅读并**理解**以下的配置文件注释！！！

<details>
  <summary><h3>❓如何编写配置❓ <h3></summary>

## ***配置***

**其中有些配置互相矛盾，请搞清逻辑关系后再进行配置！！！**

---

### **Kernel**

---

#### Kernel Source

（HTTP链接）

修改为你的内核仓库地址

例如: https://github.com/magojohnji/msm-4.14.git

支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

> Tips：此项应首选 git 仓库

#### Kernel Source Branch

（字符串）

修改为你的内核分支名称

例如: TDA，base，su，13，R，请自行查阅

#### Kernel Config

（字符串）

修改为你的内核配置文件名

例如: vendor/wayne_defconfig，vendor/violet-perf_defconfig，munch_defconfig 等

> Tips：可在内核源码的 arch/arm64/configs(/vendor) 中寻找

#### Arch

（字符串）

修改为你的 CPU 架构，一般为 arm64

例如: arm64

#### Kernel Image Name

（字符串）

修改为需要刷写的 kernel binary，一般与你的 aosp-device tree 里的 BOARD_KERNEL_IMAGE_NAME 是一致的

例如: Image.gz-dtb

常见还有 Image、Image.gz

### **Clang**

---

#### Enable Clang

（ true 或 false ）

我们提供可自定义是否开启 Clang 编译


#### Use AOSP Clang

（ true 或 false ）

可以选择是否用 AOSP 的 Clang

#### AOSP Clang Branch

（字符串）

我们提供可自定义 Google 上游分支的选项，主要的有分支有：

| Clang 分支 |
| ---------- |
| main |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

或者其它分支，请根据自己的需求在 https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 中寻找

#### AOSP Clang Version

（字符串）

填写需要使用的 Clang 版本
| Clang 版本 | 对应 Android 版本 | AOSP-Clang 版本 |
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b |
| 14.0.6 | Android T | r450784d |
| 14.0.7 | | r450784e |
| 15.0.1 | | r458507 |

***谷歌官方文档如此，但经验证个别版本无法下载，如果无法下载请设为 r450784e***

一般 Clang12 就能通过大部分 4.14 及以上的内核的编译
我自己的 Redmi Note 7 Pro (Kenrel 4.14) 使用的是 ~~r450784d~~ r450784e

> Tips：如仍提示错误，则可去 [AOSP Clang](https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86) 中寻找可用分支、版本

#### Use Custom Clang

（ true 或 false ）

可以使用除 Google 官方以外的 Clang，如 [ZyCromerZ-Clang](https://github.com/magojohnji/ZyCromerZ-Clang)

#### Custom Clang Source

（HTTP链接）

支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

> Tips：如果是 git 仓库，请填写包含`.git`的链接

#### Custom Clang Branch

（字符串）

如果使用自定义 Clang，则可自定义第三方 Clang 的分支，例如 `main`

### **GCC**

---

#### Enable GCC 

（ true 或 false ）

可以配置是否启用 GCC 交叉编译

#### Enable AOSP GCC ARM64

（ true 或 false ）

是否下载 Google 官方的 AOSP GCC，启用 GCC 64 交叉编译

如果 **`Enable GCC `** 设为false，则此项无意义

#### Enable GCC ARM32

（ true 或 false ）

是否下载 Google 官方的 AOSP GCC，启用 GCC 32 交叉编译

如果 **`Enable GCC `** 设为false，则此项无意义

#### AOSP GCC System

（字符串）

用于编译内核的系统类型

> Tips：如果使用 macOS 编译，则填写 darwin-x86

#### AOSP GCC ARM64 Version

（字符串）

顾名思义，AOSP GCC ARM64 的版本号，一般默认为 `aarch64-linux-android-4.9`

#### AOSP GCC ARM32 Version

（字符串）

顾名思义，AOSP GCC ARM32 的版本，一般默认为 `arm-linux-androideabi-4.9`

#### AOSP GCC Android Version

（字符串）

顾名思义，AOSP GCC 所对应的 Android 的版本

如：12.1.0，10.0.0

#### AOSP GCC Release

（字符串）

顾名思义，AOSP GCC 所对应的发布版本号

如：r27

> Tips：以上 AOSP Gcc 如需自定义请去 [AOSP Gcc](如需自定义请至 https://android.googlesource.com/platform/prebuilts/gcc/) 自行寻找可用分支、版本

#### Use Custom Gcc 64

（ true 或 false ）

可以配置是否使用自定义的 Gcc 64

如果 **`Enable GCC `** 设为false，则此项无意义

#### Custom Gcc 64 Source

（HTTP链接）

自定义 Gcc 64 的源代码，支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

> Tips：如果是 git 仓库，请填写包含`.git`的链接

#### Custom Gcc 64 Branch

（字符串）

如果使用自定义 Gcc 64，则可自定义第三方 Gcc 的分支，例如 `main`

#### Use Custom Gcc 32

（ true 或 false ）

可以配置是否使用自定义的 Gcc 32

如果 **`Enable GCC `** 设为false，则此项无意义

#### Custom Gcc 32 Source

（HTTP链接）

自定义 Gcc 32 的源代码，支持 git 仓库或者 zip 压缩包、tar.gz 压缩包的直链

> Tips：如果是 git 仓库，请填写包含`.git`的链接

#### Custom Gcc 32 Branch

（字符串）

如果使用自定义 Gcc 32，则可自定义第三方 Gcc 的分支，例如 `main`


### **Enable KernelSU**

（ true 或 false ）

启用 KernelSU，用于排查内核故障或单独编译内核

#### Kernel Installer

（HTTP链接）

KernelSU 的安装脚本链接，以便使用第三方版本

> Tips：
tiann 原版：https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
MlgmXyysd修改版：https://raw.githubusercontent.com/MlgmXyysd/KernelSU_Debug/master/kernel/setup.sh

#### KernelSU Branch or Tag

（字符串）

选择 KernelSU 的分支或 tag:

- main 分支(开发版): `KERNELSU_TAG=main`
- 最新 TAG(稳定版): `KERNELSU_TAG=`
- 指定 TAG(如`v0.5.2`): `KERNELSU_TAG=v0.5.2`

请自行寻找

#### KernelSU Manager signature size and hash

（字符串）

自定义KernelSU管理器签名的size值和hash值，如果不需要自定义管理器则请留空或填入官方默认值：

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=0xb0b91415`

可键入`ksud debug get-sign <apk_path>`获取apk签名的size值和hash值

#### Build KernelSU Boot IMG

（ true 或 false ）

> 从之前的 Workflows 合并进来的，可以查看历史提交

编译含KernelSU的 boot.img，需要你提供 `KernelSU Source boot image`

#### KernelSU Source Boot Image

（HTTP链接）

故名思义，提供一个源系统可以正常开机的 boot 镜像，需要直链，最好是同一套内核源码以及与你当前系统同一套设备树从 aosp 构建出来的。ramdisk 里面包含分区表以及 init，没有的话构建出来的镜像会无法正常引导。

例如: https://raw.githubusercontent.com/abc/def/main/boot/boot.img

### **Enable Magisk**

（ true 或 false ）

顾名思义，配置是否启用 Magisk

#### Magisk APK

（HTTP链接）

故名思义，提供一个 Magisk APK 文件（ZIP也可以，理论上只要是ZIP格式的文件就可以了），需要直链，支持第三方、自定义版本的 Magisk。

如果找不到官方仓库，可以去 [magisk-files-host](https://github.com/magojohnji/magisk-files-host) 找APK文件，

> Tips：拆json找链接也可以。

#### Magisk Patch Partition

（字符串）

Magisk 所修补的分区名称

一般来说，是boot分区，但不排除部分设备是 init_boot 或 vendor_boot 的可能性，详见 Magisk 官方文档。

#### Magisk Source Boot Image

（HTTP链接）

Magisk 所修补的分区的镜像文件，需要直链。

例如：https://raw.githubusercontent.com/abc/def/main/boot/boot.img

### **Build Settings**

---

#### Disable LTO

（ true 或 false ）

LTO 用于优化内核，但有些时候会导致错误

#### Disable CC_WERROR

（ true 或 false ）

用于修复某些不支持或关闭了Kprobes的内核，修复KernelSU未检测到开启Kprobes的变量抛出警告导致错误

#### Add Kprobes Config

（ true 或 false ）

自动在 defconfig 注入参数，启用 Kprobes 支持

#### Add overlayfs Config

（ true 或 false ）

为 KernelSU 模块和 system 分区读写提供支持，自动在 defconfig 注入参数

#### Enable ccache

（ true 或 false ）

启用缓存，让第二次编译内核更快，最少可以减少 2/5 的时间

#### Need DTBO

（ true 或 false ）

上传 DTBO
部分设备需要

#### Extra cmds

（字符串）

有的内核需要加入一些其它编译命令，才能正常编译，一般不需要其它的命令，请自行搜索自己内核的资料
请在命令与命令之间用空格隔开

例如: LLVM=1 LLVM_IAS=1

#### TC Custom cmds

（字符串）

编译工具链配置，~~自己改改这些配置应该都会吧 :)~~ 自行询问内核作者或分析内核编译脚本

## ***有用的技巧***（恭喜你读完了 **`配置`** 部分）

- 如果想要在修改文件后自动构建，则可以将 [build-kernel.yml](.github/workflows/build-kernel.yml) 的开头部分改成这样：

```yaml
name: Build
on:
  push:
    branches: [ main ]
  workflow_dispatch:
    inputs:
      release:
        description: "Release"
        required: true
        default: false
        type: boolean

```

- 如果想要每天定时编译，则可以将 [build-kernel.yml](.github/workflows/build-kernel.yml) 的开头部分改成这样：

（每天 2:00 UTC 执行）

```yaml
name: Build
on:
  schedule:
    - cron: "0 2 * * *"
  workflow_dispatch:
    inputs:
      release:
        description: "Release"
        required: true
        default: false
        type: boolean
```

当然你也可以将他们混合起来 :-)

</details>

## 其他

如果你有发现无法运行的情况，或需要添加、修改功能，请提出 **[Issue](https://github.com/magojohnji/Add_KernelSU-Magisk_Action/issues)** 来让我知道！

## 感谢

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [tiann](https://github.com/tiann)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)

## LICENSE

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