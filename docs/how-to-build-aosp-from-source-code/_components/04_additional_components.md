## **Prepare additional components**

!!! warning "Notice"
	Please download `RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software.zip` package that includes addtitional components.

[:octicons-download-16: RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software.zip](https://www.renesas.com/en/document/sws/rzg3l-software-package-aosp-17-proprietary-software){ .md-button .btn-round target=_blank }

### Hardware Codec module

By default, Hardware Codecs related repos are not included in source tree. Because no license agreement is confirmed.

- Software codecs are used as default.
- No additional repositories are required.

See [How to extract additional components](#how-to-extract-additional-components) to add Hardware Codec modules to your RZ AOSP build environment before building Android images

!!! note
	 Please export `ENABLE_HW_CODECS=true` before building Android images

### Extract Wi-Fi firmware

By default, Wi-Fi firmware is not included in source tree.

See [How to extract additional components](#how-to-extract-additional-components) to add firmware for Wi-Fi to your RZ AOSP build environment before building Android images

!!! note
	- Please export `ENABLE_WIFI_SUPPORT=true` before building Android images
	- For enabling Wi-Fi support, please see [Wi-Fi usage](../application-notes/#wi-fi-usage)

### How to extract additional components

Ensure that you have get RZ AOSP source code successfully. See [Get RZ AOSP source code](#get-rz-aosp-source-code)

Jump to your android build directory

```bash
cd ${ANDROID_BUILD_DIR}
```
{: .dollar }

Extract the `RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software.zip` package

```bash
unzip <path to proprietary software package>/RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software.zip -d .
```
{: .dollar }

Confirm the content of `RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software`

```bash
tree -L 1 ${ANDROID_BUILD_DIR}/RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software
```
{: .dollar }

The content should be:
```text
RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software
├── apply_package.sh
├── mydroid
└── README.txt
```

Copy the `RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software` package to your workspace

```bash
cp -rf ${ANDROID_BUILD_DIR}/RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software ${workspace}/
```
{: .dollar }

Jumping to `RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software` directory

```bash
cd ${workspace}/RTK0EF0188Z78001ZJ_v17.0.0_proprietary-software
```
{: .dollar }

Run below script to apply additional components to your RZ AOSP environment

```bash
./apply_package.sh
```
{: .dollar }
