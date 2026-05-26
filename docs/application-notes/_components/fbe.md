## **Enable File-Based Encryption**

File-based encryption allows different files to be encrypted with different keys that can be unlocked independently.

By default, we disabled encryption to reduce the booting time. In case that users want to enable encryption support, please **export ENABLE_FBE=true**, rebuild and re-flash Android images see [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources) and [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot))

Please note that the booting time with encryption support may rarely take around 1 ~ 3 minutes for encrypt/decrypt data.

<span style="color:red">**Note:**</span> File-Based Encryption is disabled by default. All supported features were tested under this configuration
