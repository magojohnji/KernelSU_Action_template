[Chinese (Simplified)](README_ZH-HANS.md) | [Chinese (Traditional)](README_ZH-HANT.md) | **English**

# Add KernelSU and Magisk Action

The ***Plus*** version, can compile kernel, AnyKernel3, boot-kernelsu.img, boot-magisk.img, magisk.zip

Compiling the Action of the Non-GKI kernel has a certain degree of universality.

## Support Kernels

- `5.4`
- `4.19`
- `4.14`
- `4.9`

## Usage

> After the compilation is successful, a series of content such as AnyKernel3 will be uploaded in `Action`, and the device check has been closed. Please ensure that the phone is unlocked before flashing in!

- Fork this warehouse, edit the configuration according to config.env.xx-xx.simple (your language), or open the documents folder to view the document, and then open [kernel-build.yml](.github/workflows/build-kernel.yml ), modify the configuration file name on line 32.

- Then enter Actions, click on the option, you will see `Run workflows` on the top of the large dialog box on the right, click it to start the build.

*If Release is checked, Release will be released.*

## Grateful

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
- [topjohnwu](https://github.com/topjohnwu)
- [xiaoxindada](https://github.com/xiaoxindada)
- [Tonyha](https://github.com/Tonyha7)
- [action](https://github.com/action)