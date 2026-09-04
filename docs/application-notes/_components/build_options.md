## **Android build options**

AOSP 17 supports many lunch combos. Users can freely choose them based on their target. Please refer to below build options:

<div class="table-no-sort" markdown="1">
| Build option | Lunch command | board_name | Note |
| :--- | :--- | :--- | :--- |
| **Base** | `lunch smarc_rzg3l-cp2a-userdebug` | smarc_rzg3l | Base environment based on pure AOSP. No demo applications.|
| Demo | `lunch smarc_rzg3l_demo-cp2a-userdebug` | smarc_rzg3l | Inherit base build option. But it has some demo applications. |
</div>

!!! note
    * Please update “board_name” based on lunch command before copying Android images (See [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources))
    * This release is fully tested for “Base” build option. Other build options are <span style="color:red">NOT</span> fully tested yet.
