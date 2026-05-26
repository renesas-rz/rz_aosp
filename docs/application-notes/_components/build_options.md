## **Android build options**

AOSP 15 supports many lunch combos. Users can freely choose them based on their target. Please refer to below build options:

<div class="table-no-sort" markdown="1">
| Build option | Lunch command | board_name | Note |
| :--- | :--- | :--- | :--- |
| Minimal | `lunch rzv2h_evk_ver1_minimal-ap4a-userdebug` | rzv2h_evk_ver1 | No hardware codecs support, less application, no demo applications, no experiment features. Reserved more free memory. |
| **Base** | `lunch rzv2h_evk_ver1-ap4a-userdebug` | rzv2h_evk_ver1 | Base environment based on pure AOSP. No demo applications.|
| Demo | `lunch rzv2h_evk_ver1_demo-ap4a-userdebug` | rzv2h_evk_ver1 | Inherit base build option. But it has some demo applications. |
</div>

<span style="color:red">**Note:**</span>

* Please update “board_name” based on lunch command before copying Android images (See [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources))
* This release is fully tested for “Base” build option. Other build options are <span style="color:red">NOT</span> fully tested yet.
