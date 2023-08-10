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

- Star 本倉庫，然後 Fork 本倉庫，以確保工作流運行正常。

- 按照 config.env.xx-xx.simple （你的語言）編輯配置，然後將配置文件改名為config_xxxx.env，***必須***以 `.env` 結尾！
後打開 [kernel-build.yml](.github/workflows/build-kernel.yml)，修改第32行的配置文件名稱。

- 之後進入 Actions，點擊選項會看見右邊的大對話框的上面會有`Run workflows`，點擊它會啟動構建。

- 若勾選 Release，則會發布 Release

## 其他

如果你有發現無法運行的情況，或需要添加、修改功能，請提出 **[Issue](https://github.com/magojohnji/Add_KernelSU-Magisk_Action/issues)** 來讓我知道！

## 感謝

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)