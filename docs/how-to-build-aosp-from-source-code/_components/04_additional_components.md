## **Prepare additional components**

!!! warning "Notice"
	Please download `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software.zip` package that includes addtitional components.

[:octicons-download-16: RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software.zip](https://www.renesas.com/en/document/sws/rzv2h-software-package-aosp-15-proprietary-software){ .md-button .btn-round target=_blank }

### Mali Graphics module (**Mandatory to boot up**)

By default, Mali Graphics modules is not included in source tree. Because no license agreement is confirmed.

See [How to extract additional components](#how-to-extract-additional-components) to add Mali Graphics modules to your RZ AOSP build environment before building Android images

<span style="color:red">**Note:**</span>

- This repo is required to boot with Mali Graphics successfully. If users skip it, users must check how to switch to use mesa Graphics.
- Officially, All features have been tested with Mali Graphics.
- Please run `vendor/arm/gralloc/configure` before building Android images

### Hardware Codec module

By default, Hardware Codecs related repos are not included in source tree. Because no license agreement is confirmed.

- Software codecs are used as default.
- No additional repositories are required.

See [How to extract additional components](#how-to-extract-additional-components) to add Hardware Codec modules to your RZ AOSP build environment before building Android images

<span style="color:red">**Note:**</span> Please export `ENABLE_HW_CODECS=true` before building Android images

### USB Wi-Fi module

By default, USB Wi-Fi kernel module is not included in source tree.

See [How to extract additional components](#how-to-extract-additional-components) to add USB Wi-Fi modules to your RZ AOSP build environment before building Android images

<span style="color:red">**Note:**</span> Please export `USE_USB_WIFI=true` before building Android images

### How to extract additional components

Ensure that you have get RZ AOSP source code successfully. See [Get RZ AOSP source code](#get-rz-aosp-source-code)

Jump to your android build directory
```bash
$ cd ${ANDROID_BUILD_DIR}
```

Extract the `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software.zip` package
```bash
$ unzip <path to proprietary software package>/RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software.zip -d .
```

Confirm the content of `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software`
```bash
$ tree -L 1 ${ANDROID_BUILD_DIR}/RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software
```

The content should be:
```text
RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software
├── apply_package.sh
├── mydroid
├── patch_OV5645
└── README.txt
```

Copy the `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software` package to your workspace
```bash
$ cp -rf ${ANDROID_BUILD_DIR}/RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software ${workspace}/
```

Jumping to `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software` directory
```bash
$ cd ${workspace}/RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software
```

Run below script to apply additional components to your RZ AOSP environment
```bash
$ ./apply_package.sh
```

### MIPI Camera module

By default, the MIPI Camera is not enabled in the kernel. Because the CMOS sensor (OV5645) in the MIPI camera is no longer available and should not be used for mass production. Any software support provided is for evaluation purposes only.

Ensure that you have downloaded `RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software.zip` package from renesas.com

Jumping to kernel
```bash
$ cd ${workspace}/mydroid/device/renesas/kernel
```

Apply the MIPI Camera support patches to kernel
```bash
$ git am ${workspace}/RTK0EF0188Z76001ZJ_v15.3.0_proprietary-software/patch_OV5645/android15_6.1-cip28-base-update1/*.patch
```

<span style="color:red">**Note:**</span> Please build new Android image after applying MIPI Camera support patches
