**中文（简体）** | [中文（繁體）](README_ZH-HANT.md) | [English](README_EN-US.md)

# Add KernelSU and Magisk Action

***Plus***版本，可以编译内核、AnyKernel3、boot-kernelsu.img、boot-magisk.img、magisk.zip

编译 Non-GKI 内核 的 Action，具有一定的普遍性。

## 支持内核

- `5.4`
- `4.19`
- `4.14`
- `4.9`

## 使用

> 编译成功后，会在`Action`上传 AnyKernel3 等一系列内容，已经关闭设备检查，请确保手机已经解锁后再刷入！

Fork 本仓库，按照 config.env.xx-xx.simple （你的语言）编辑配置，或打开 documents 文件夹查看文档，后打开 [kernel-build.yml](.github/workflows/build-kernel.yml)，修改第32行的配置文件名称。

之后进入 Actions，点击选项会看见右边的大对话框的上面会有`Run workflows`，点击它会启动构建。

若勾选 Release，则会发布 Release

## 感谢

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)