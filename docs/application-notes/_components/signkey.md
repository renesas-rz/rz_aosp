## **How to sign release keys for Android images**

When user wants to perform CTS/VTS testing or sign keys for final product, please refer this part to sign keys for Android images.

!!! note
    generate-signed-img.sh script contains some specific information that is related to Renesas. Please update if needed.

Go to your `mydroid` directory
```bash
cd ${workspace}/mydroid
```
{: .dollar }


Copy signed keys script to your mydroid
```bash
cp ${workspace}/RELFILES/tools/generate-signed-img.sh .
```
{: .dollar }


Export all necessary build variables
```bash
export TARGET_BOARD_PLATFORM=r9a09g057h4-evk
source build/envsetup.sh
```
{: .dollar }


Please see more lunch build options at [Android build options](#android-build-options).
Assume that you are signing key for Android “user” build images (build option is “base”), run below commands:
```bash
lunch rzv2h_evk_ver1-ap4a-user
```
{: .dollar }


Run below command to sign keys. Input your password or blank for non-password. Press "Enter" to continue.
```bash
chmod 777 generate-signed-img.sh
./generate-signed-img.sh
```
{: .dollar }


Confirm any missing APKs or APEXs not signed with new own release keys:
```bash
check_target_files_signatures -l .android-certs signed-target_files_rzv2h_evk_ver1.zip
```
{: .dollar }


Copy output into **image_dir** ([Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources)). Please export **images_dir** before copying images
```bash
export images_dir=<your_images_dir>
```
{: .dollar }


Overwrite with the signed images
```bash
unzip signed-img_rzv2h_evk_ver1.zip -d ${image_dir}
```
{: .dollar }


Re-flash Android images ([Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot))

!!! note
    Enable USB Debugging in Developer options to use adb.

To confirm whether new images are signed keys:

On host PC, bellow command should show release-keys (example: RZ/V2H):
```bash
adb shell getprop | grep 'ro.build.fingerprint'
```
{: .dollar }

```bash
[ro.build.fingerprint]:[Renesas/rzv2h_evk_ver1/rzv2h_evk_ver1:15/BP1A.250305.020.T2/eng.khoang:user/releasekeys]
```
{: .hash}

On host PC, bellow command should show **no result**
```bash
adb shell getprop | grep 'test-keys'
```
{: .dollar }

