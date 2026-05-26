### **Note**

| No. | Note |
| :---: | :--- |
| 1 | <span style="color:red">**Important note:**</span> This RZ AOSP 15 only supports arm64-v8a (64-bit only) as primary architecture. No secondary architecture (**armeabi-v7a**) (32-bit) support. So, users can only install applications which support **arm64-v8a**. |
| 2 | It’s <span style="color:red">**NOT**</span> recommended to hot-plug HDMI. It may cause the board broken. |
| 3 | This release is fully tested for “Base” build option. Other build options are <span style="color:red">**NOT**</span> fully tested. |
| 4 | It's required to disable "Auto Select" feature on monitor to disable auto scanning input. |
| 5 | It's required to plug external power if users use external devices like portable monitor, USB hub..., etc. |
| 6 | No support external storage on SD1 slot when booting Android image by SD card on SD2 slot. |
| 7 | codec_bin partition won’t be updated during OTA update|
| 8 | Some .aac audio files might show the wrong total time. Known limitation with inaccurate duration reporting for raw AAC (ADTS) files due to Variable Bitrate (VBR) characteristics|
