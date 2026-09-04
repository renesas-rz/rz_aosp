# FAQ

If you have any questions about RZ AOSP BSP, please create an issue at:

[GitHub Issues](https://github.com/renesas-rz/rz_aosp/issues){: target="_blank" }: For technical questions, bug reports, or feature requests related to RZ AOSP.

!!! note
    A GitHub account is required to create an issue.

---

### Q1. How to add new package to RZ AOSP BSP?

Please find package name from Android.mk

![](images/LOCAL_MODULE_Androidmk.png)

or Android.bp

![](images/name_Androidbp.png)

Then please add package name to `${workspace}/mydroid/device/renesas/common/DeviceCommon.mk` like below:
```bash
PRODUCT_PACKAGES += \
    android.hardware.media.c2-service.renesas \
    android.hardware.health-service.renesas 
```

!!! note
     It's required to write SELinux policies for these packages, please refer to [Security-Enhanced Linux in Android](https://source.android.com/docs/security/features/selinux/device-policy){: target="_blank" }

### Q2. How to copy file to RZ AOSP BSP?

Example: Copying file `${workspace}/mydroid/device/renesas/common/fstab.sdboot_slot1` to vendor partition (/vendor/) after booting.
Please add below contents to `${workspace}/mydroid/device/renesas/common/DeviceCommon.mk`:
```bash
PRODUCT_COPY_FILES += \
    device/renesas/common/fstab.sdboot_slot1:$(TARGET_COPY_OUT_VENDOR)/etc/fstab.sdboot_slot1
```
See more examples at `${workspace}/mydroid/device/renesas/common/DeviceCommon.mk`

### Q3. How to change display resolution?

Please check [Booting with video parameter set](../application-notes/#booting-with-video-parameter-set)

### Q4. What to do if fetch stage is not sucess?

When executing the fetch commands from [Get RZ AOSP source code](../how-to-build-aosp-from-source-code/index.md#get-rz-aosp-source-code)
It may meet trouble with `repo sync` in step 

```bash
./walkthrough.sh SMARC_RZG3L
```
{: .dollar }

Typical online fetch errors may include:

!!! danger "Error log"
    error: RPC failed <br>
    fatal: unable to access <br>
    fatal: early EOF <br>
    GitError: fetch failed <br>
    HTTP 403 <br>
    HTTP 500 <br>
    The remote end hung up unexpectedly <br>

#### Workaround:

```bash
cd <working_dir>/mydroid
repo sync -j$(nproc)
```
{: .dollar }

!!! note
    Using an AOSP mirror is recommended to improve fetch reliability and build stability. Please check [Q5. Using AOSP mirror for offline fetch](#q5-using-aosp-mirror-for-offline-fetch)



### Q5. Using AOSP mirror for offline fetch

#### When should users use the AOSP mirror?

Use the AOSP mirror (Offline for AOSP parts. For RZ parts, it requires internet access) when:

- `repo init` or `repo sync` repeatedly fails while accessing online AOSP repositories.
- The build environment has limited or unstable Internet access.
- A proxy, firewall, or shared external IP causes intermittent fetch errors.
- The project requires a more stable and repeatable source-fetch flow.

Before switching sources, retrying `repo sync` may resolve a temporary network failure. If the errors continue, use the internal mirror.

#### How to prepare an AOSP mirror?

Please follow guide from <https://source.android.com/docs/setup/download/troubleshoot-sync#use-mirror> to download AOSP mirror

---

#### How to use the AOSP mirror with aosp_local_package (RZ AOSP) which was downloaded from [Get RZ AOSP source code](../how-to-build-aosp-from-source-code/index.md#get-rz-aosp-source-code)?

Step 1: Make sure the mirror is accessible

Verify access (Example: AOSP mirror was placed at $WORK_DIR/aosp_mirror)

```bash
export WORK_DIR=`pwd`
ls $WORK_DIR/aosp_mirror
```
{: .dollar }

---

Step 2: Configure aosp_local_package which was downloaded from [Clone android local package](../how-to-build-aosp-from-source-code/index.md#get-rz-aosp-source-code)

Update the platform configuration to enable offline fetch mode in `buildenv.sh`.

Example:

```bash
USE_MIRROR="YES"
LOCAL_MIRROR_DIR=$WORK_DIR/aosp_mirror
```

---

Step 3: Run fetch operation

Continue executing the step `./walkthrough.sh SMARC_RZG3L` from [Get RZ AOSP source code](../how-to-build-aosp-from-source-code/index.md#get-rz-aosp-source-code)

---




