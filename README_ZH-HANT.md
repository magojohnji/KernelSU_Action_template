[中文（简体）](README_ZH-HANS.md) | **中文（繁體）** | [English](README_EN-US.md)

# Add KernelSU and Magisk Action

***Plus***版本，可以編譯內核、AnyKernel3、boot-kernelsu.img、boot-magisk.img、magisk.zip

編譯 Non-GKI 內核 的 Action，具有一定的普遍性。

## 支持內核

- `5.4`
- `4.19`
- `4.14`
- `4.9`

## 使用

> 編譯成功後，會在`Action`上傳 AnyKernel3 等一系列內容，已經關閉設備檢查，請確保手機已經解鎖後再刷入！

Fork 本倉庫，按照config.env.xx-xx.simple （你的語言）編輯配置，或打開documents 文件夾查看文檔，後打開[kernel-build.yml](.github/workflows/build-kernel.yml )，修改第32行的配置文件名稱。

之後進入 Actions，點擊選項會看見右邊的大對話框的上面會有`Run workflows`，點擊它會啟動構建。

若勾選 Release，則會發布 Release

## 感謝

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)