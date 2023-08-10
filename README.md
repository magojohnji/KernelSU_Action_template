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

- Star this repo, then fork this repo to make sure the workflow works fine.

- Edit the configuration according to config.env.xx-xx.simple (your language), then rename the configuration file to config_xxxx.env, ***must*** end with `.env`!
Then open [kernel-build.yml](.github/workflows/build-kernel.yml) and modify the configuration file name on line 32.

- Then enter Actions, click the option, you will see `Run workflows` on the top of the large dialog box on the right, click it to start the build.

- If Release is checked, Release will be released

## Other

If you find something that doesn’t work, or you need to add or modify functions, please raise **[Issue](https://github.com/magojohnji/Add_KernelSU-Magisk_Action/issues)** to let me know!

## Grateful

- [xiaoleGun](https://gitjin.com/xiaoleGun)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://android.googlesource.com)
- [KernelSU](https://github.com/tiann/KernelSU)
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