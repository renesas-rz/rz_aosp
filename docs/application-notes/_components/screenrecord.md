## **Screen Record issue from Quick Settings**

Using the Screen Record application accessed from Quick Settings may lead to a soft reboot on devices running in an FBE (File-Based Encryption) environment. This issue is caused by a poor implementation in the AOSP source code, where processing the output recording file blocks the main UI thread and leads to system instability.

To resolve this, please apply the following patch to handle the processing more efficiently and prevent the device from rebooting unexpectedly during stopping recording, by moving processing recording output to background thread and let UI response immediately.

```bash
$ cd ${workspace}/mydroid/frameworks/base
$ git am ${workspace}/additional_patches/0001-frameworks-base-Fix-failed-to-stop-record-by-Screen-.patch
$ cd ${workspace}/mydroid
```
Rebuild and re-flash Android images (See [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources) and [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot)).

<span style="color:red">**Note:**</span>

- This patch has improved the issue and rarely see it while continuous recording.
- While the recording output is being saved, the system may take longer to launch new applications.
