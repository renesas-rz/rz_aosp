## **OTA (over-the-air) update**

### Building full OTA package

* Make sure to export build variables which were used to build previous images:

* On Host PC, jump to your `mydroid` directory
```bash
cd ${workspace}/mydroid
```
{: .dollar }


* Export build variables:
```bash
source build/envsetup.sh
lunch <Please use the same lunch combo as the original image>
```
{: .dollar }


!!! note
    Users should export build variables properly before building OTA packages.

* Build OTA package following the command below:

On Host PC, execute below commands:
```bash
mkdir dist_output
make dist DIST_DIR=dist_output
```
{: .dollar }


* Full OTA package for each board will be located at:
```text
${workspace}/mydroid/out/target/product/${CUT_TARGET_PRODUCT}/${TARGET_PRODUCT}-ota.zip
```

!!! note
    For more detail about building Android images, please read [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources).

### Installing OTA packages

There are 3 methods to update OTA packages:

**Method 1) Apply update from ADB:**

* On Host PC, jump to your `mydroid`
```bash
cd ${workspace}/mydroid
```
{: .dollar }


* Accessing to Recovery mode:
```bash
./out/host/linux-x86/bin/adb reboot recovery

```
{: .dollar }

* In case multiple devices were plugged in PC please provide serial number:
```bash
./out/host/linux-x86/bin/adb -s <serialno> reboot recovery
```
{: .dollar }

* Choosing **Apply update from ADB** on Recovery GUI (using touch screen to swipe UP, DOWN, RIGHT (select) or use a physical keyboard).

* Install OTA package:
```bash
./out/host/linux-x86/bin/adb sideload <your full OTA package>
```
{: .dollar }

* In case multiple devices were plugged in PC please provide serial number:
```bash
./out/host/linux-x86/bin/adb -s <serialno> sideload <your full OTA package>
```
{: .dollar }


* Waiting for progress 100%. Android screen will show:
```text
Install from ADB completed with status 0
```

* Then choose “Reboot system now” on Recovery GUI (skip if used sideload-auto-reboot).

* Users need to wait for update engine to complete cleanup process in the first boot after OTA update. If user wants to make sure the update is completed via logcat, the log should be:
```text
update_engine: [...] Waiting for merge to complete: 99%.
update_engine: [...] Removing all update state.
update_engine: [...] Merge finished with state MergeCompleted.
```

**Method 2) Apply update from SD card:**

* Please copy your full OTA package zip file to SD Card

* On Host PC, jump to your `mydroid`
```bash
cd ${workspace}/mydroid
```
{: .dollar }


* Accessing to Recovery mode:
```bash
./out/host/linux-x86/bin/adb reboot recovery
```
{: .dollar }
* In case multiple devices were plugged in PC please provide serial number:
```bash
./out/host/linux-x86/bin/adb -s <serialno> reboot recovery
```
{: .dollar }


* Choosing **Apply update from SD card** on Recovery GUI (using touch screen to swipe UP, DOWN, RIGHT (select) or use a physical keyboard). Then choose your full OTA package.

* Waiting for progress 100%. Android screen will show:
```text
Install from SD card completed with status 0
```

* Then choose “Reboot system now” on Recovery GUI.

* Users need to wait for update engine to complete cleanup process in the first boot after OTA update. If user wants to make sure the update is completed via logcat, the log should be:
```text
update_engine: [...] Waiting for merge to complete: 99%.
update_engine: [...] Removing all update state.
update_engine: [...] Merge finished with state MergeCompleted.
```

**Method 3) Apply update from SystemUpdaterSample application:**

* On Host PC, jump to your `mydroid`
```bash
cd ${workspace}/mydroid
```
{: .dollar }


* Creating OTA configuration file (Make sure to export build variables before)
```bash
source build/envsetup.sh
lunch <Please use the same lunch combo as the original image>
```
{: .dollar }


* Make sure to install the protobuf package (version 3.20.1)
```bash
pip3 install --target build/make/tools/releasetools --force-reinstall "protobuf==3.20.1"
```
{: .dollar }

!!! note
    Recommended python3 version: 3.8.10

* Create OTA configuration file following below command:
```bash
make full_ota_config
```
{: .dollar }


* OTA configuration file will be located at:
```text
${workspace}/mydroid/${TARGET_PRODUCT}-config.json
```

* Make sure your Host PC can detect your Android device via adb. Use below commands:
```bash
./out/host/linux-x86/bin/adb devices
```
{: .dollar }


* Push the full OTA package and the OTA configuration file to Android device
```bash
export CONFIG_DIR="/data/user/0/com.example.android.systemupdatersample/files/configs"
export FILE_DIR="/data/user/0/com.example.android.systemupdatersample/files"
./out/host/linux-x86/bin/adb root
```
{: .dollar }


* Push full OTA package
```bash
./out/host/linux-x86/bin/adb push ${workspace}/mydroid/out/target/product/${TARGET_PRODUCT}/${TARGET_PRODUCT}-ota.zip $FILE_DIR/
```
{: .dollar }
* Push OTA configuration file
```bash
./out/host/linux-x86/bin/adb push ${workspace}/mydroid/${TARGET_PRODUCT}-config.json $CONFIG_DIR/
```
{: .dollar }

* In case multiple devices were plugged in PC please provide serial number:
```bash
./out/host/linux-x86/bin/adb -s <serialno> root
./out/host/linux-x86/bin/adb push -s <serialno> ${workspace}/mydroid/out/target/product/${TARGET_PRODUCT}/${TARGET_PRODUCT}-ota.zip $FILE_DIR/
./out/host/linux-x86/bin/adb push -s <serialno> ${workspace}/mydroid/${TARGET_PRODUCT}-config.json $CONFIG_DIR/
```
{: .dollar }


* You can check the input files on Android device manually.<br>
Your OTA package will be located at:
```text
/data/user/0/com.example.android.systemupdatersample/files/${TARGET_PRODUCT}-ota.zip
```
Your OTA configuration file will be located at:
```test
/data/user/0/com.example.android.systemupdatersample/files/configs/${TARGET_PRODUCT}-config.json
```

* Disable SELinux before applying full OTA package
```bash
./out/host/linux-x86/bin/adb shell setenforce 0
```
{: .dollar }


* In case multiple devices were plugged in PC please provide serial number:
```bash
./out/host/linux-x86/bin/adb -s <serialno> shell setenforce 0
```
{: .dollar }


* Open SystemUpdaterSample application and click **RELOAD** button, then application will show up your OTA configuration file. You could re-check your configuration again before going to the next step.
<p align="center">
  <img src="images/system_updater_sample.png" alt="System Updater Sample" width="100%">
</p>


* Click **APPLY** button to start OTA progress update. The logs when the OTA package is installed successfully will look like this:
```text
Update state: REBOOT_REQUIRED/5
Engine status: UPDATED_NEED_REBOOT/6
Engine error: SUCCESS/0
```
!!! note
    If you want to switch slot automatically without rebuilding OTA configuration file, you could tick `Automatically switch slot on next boot` checkbox, prior to click **APPLY** button. This option is not mandatory.

* Reboot Android device after OTA package was installed successfully.


* Users need to wait for update engine to complete cleanup process in the first boot after OTA update. If user wants to make sure the update is completed via logcat, the log should be:
```text
update_engine: [...] Waiting for merge to complete: 99%.
update_engine: [...] Removing all update state.
update_engine: [...] Merge finished with state MergeCompleted.
```
