## **Fastboot UDP**

In this release, we provide fastboot UDP which uses UDP protocol to flash Android image. Alternatively, users can run fastboot protocol over Ethernet cable if USB is not available.

By default, fastbootd is supported for fastboot USB. If user wants to use fastboot UDP for flashing Android images, please **export USE\_FASTBOOTD\_FOR\_UDP=true** then rebuild and re-flash Android
images (See [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources) and [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot)).

| No. | Issue/Limitation |
| :--- | :--- |
| 1 | Do NOT support “fastboot devices” command.|
| 2 | Fastboot messages are not shown properly. |

<span style="color:red">**Note:**</span>

- Fastboot USB does <span style="color:red">**NOT**</span> work after enabling fastbootd for fastboot UDP
- Fastboot UDP does <span style="color:red">**NOT**</span> work on Ethernet port (CN6).
