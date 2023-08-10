### Config Env

顧名思義，配置文件的名稱

### Kernel Source

修改為你的內核倉庫地址

例如: https://github.com/Diva-Room/Miku_kernel_xiaomi_wayne.git

> 如果是 git 倉庫，請填寫包含`.git`的鏈接

支持 git 倉庫或者 zip 壓縮包、tar.gz 壓縮包的直鏈

### Kernel Source Branch

修改為你的內核分支

例如: TDA

### Kernel Config

修改為你的內核配置文件名

例如: vendor/wayne_defconfig

### Arch

例如: arm64

### Kernel Image Name

修改為需要刷寫的 kernel binary，一般與你的 aosp-device tree 裡的 BOARD_KERNEL_IMAGE_NAME 是一致的

例如: Image.gz-dtb

常見還有 Image、Image.gz

### Clang

#### Enable Clang

由於 [#75](https://github.com/xiaoleGun/KernelSU_Action/issues/75) 的需要，我們提供可自定義 是否開啟 Clang 編譯

可以選擇是否開啟 Clang 編譯

#### Use AOSP Clang

可以選擇是否用 AOSP 的 Clang

#### AOSP Clang Branch

由於 [#23](https://github.com/xiaoleGun/KernelSU_Action/issues/23) 的需要，我們提供可自定義 Google 上游分支的選項，主要的有分支有
| Clang 分支 |
| ---------- |
| master |
| master-kernel-build-2021 |
| master-kernel-build-2022 |

或者其它分支，請根據自己的需求在 https://android.googlesource.com/platform/prebuilts/clang/host/linux-x86 中尋找

#### AOSP Clang Version

填寫需要使用的 Clang 版本
| Clang 版本 | 對應 Android 版本 | AOSP-Clang 版本 |
| ---------- | ----------------- | --------------- |
| 12.0.5 | Android S | r416183b |
| 14.0.6 | Android T | r450784d |
| 14.0.7 | | r450784e |
| 15.0.1 | | r458507 |

***谷歌官方文檔如此，但經驗證個別版本無法下載***

一般 Clang12 就能通過大部分 4.14 及以上的內核的編譯
我自己的 MI 6X 4.19 使用的是 ~~r450784d~~ r450784e

#### Use Custom Clang

可以使用除 Google 官方的 Clang，如[ZyCromerZ-Clang](https://github.com/magojohnji/ZyCromerZ-Clang)

#### Custom Clang Source

> 如果是 git 倉庫，請填寫包含`.git`的鏈接

支持 git 倉庫或者 zip 壓縮包、tar.gz 壓縮包的直鏈

#### Custom Clang Branch

自定義第三方 Clang 的分支，例如 `main`

### GCC

#### Enable GCC 

啟用 GCC 交叉編譯

#### Enable AOSP GCC ARM64

下載 Google 官方的 AOSP GCC，啟用 GCC 64 交叉編譯

#### Enable GCC ARM32

下載 Google 官方的 AOSP GCC，啟用 GCC 32 交叉編譯

#### AOSP GCC System

用於編譯內核的系統類型

如果使用 macOS 編譯，則填寫 darwin-x86

#### AOSP GCC ARM64 Version

顧名思義，AOSP GCC ARM64 的版本

#### AOSP GCC ARM32 Version

顧名思義，AOSP GCC ARM32 的版本

#### AOSP GCC Android Version

顧名思義，AOSP GCC 所對應的 Android 的版本

#### AOSP GCC Release

顧名思義，AOSP GCC 所對應的 Android 的版本發布版本

### Enable KernelSU

啟用 KernelSU，用於排查內核故障或單獨編譯內核

#### Kernel Installer

KernelSU 的安裝腳本鏈接，以便使用第三方版本

例如：tiann 原版：https://raw.githubusercontent.com/tiann/KernelSU/main/kernel/setup.sh
      MlgmXyysd修改版：https://raw.githubusercontent.com/MlgmXyysd/KernelSU_Debug/master/kernel/setup.sh

#### KernelSU Branch or Tag

選擇 KernelSU 的分支或 tag:

- main 分支(開發版): `KERNELSU_TAG=main`
- 最新 TAG(穩定版): `KERNELSU_TAG=`
- 指定 TAG(如`v0.5.2`): `KERNELSU_TAG=v0.5.2`

#### KernelSU Manager signature size and hash

自定義KernelSU管理器簽名的size值和hash值，如果不需要自定義管理器則請留空或填入官方默認值：

`KSU_EXPECTED_SIZE=0x033b`

`KSU_EXPECTED_HASH=0xb0b91415`

可鍵入`ksud debug get-sign <apk_path>`獲取apk簽名的size值和hash值

### Build KernelSU Boot IMG

> 從之前的 Workflows 合併進來的，可以查看歷史提交

編譯含KernelSU的 boot.img，需要你提供`KernelSU Source boot image`

### KernelSU Source Boot Image

故名思義，提供一個源系統可以正常開機的 boot 鏡像，需要直鏈，最好是同一套內核源碼以及與你當前系統同一套設備樹從 aosp 構建出來的。 ramdisk 裡麵包含分區表以及 init，沒有的話構建出來的鏡像會無法正常引導。

例如: https://raw.githubusercontent.com/xiaoleGun/KernelSU_action/main/boot/boot-wayne-from-Miku-UI-latest.img

### Enable Magisk

顧名思義，配置是否啟用 Magisk

### Magisk APK

故名思義，提供一個 Magisk APK 文件（ZIP也可以，理論上只要是ZIP格式的文件就可以了），需要直鏈，支持第三方、自定義版本的 Magisk。

如果找不到官方倉庫，可以去 [magisk-files-host](https://github.com/magojohnji/magisk-files-host) 找APK文件，

拆json找鏈接也可以。

### Magisk Patch Partition

Magisk 所修補的分區名稱

一般來說，是boot分區，但不排除部分設備是 init_boot 或 vendor_boot 的可能性，詳見 Magisk 官方文檔。

### Magisk Source Boot Image

Magisk 所修補的分區的鏡像文件，需要直鏈。

### Disable LTO

LTO 用於優化內核，但有些時候會導致錯誤

### Disable CC_WERROR

用於修復某些不支持或關閉了Kprobes的內核，修復KernelSU未檢測到開啟Kprobes的變量拋出警告導致錯誤

### Add Kprobes Config

自動在 defconfig 注入參數

### Add overlayfs Config

此參數為 KernelSU 模塊和 system 分區讀寫提供支持
自動在 defconfig 注入參數

### Enable ccache

啟用緩存，讓第二次編譯內核更快，最少可以減少 2/5 的時間

### Need DTBO

上傳 DTBO
部分設備需要

### Extra cmds

有的內核需要加入一些其它編譯命令，才能正常編譯，一般不需要其它的命令，請自行搜索自己內核的資料
請在命令與命令之間用空格隔開

例如: LLVM=1 LLVM_IAS=1

### TC Custom cmds

編譯工具鏈配置，自己改改這些配置應該都會吧 :)