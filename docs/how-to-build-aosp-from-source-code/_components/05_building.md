## **Building Android, IPL, U-Boot, and Kernel sources**

!!! danger "Caution"
	It's required to download and extract additional components to build RZ AOSP.
	Please refer [Prepare additional components](#prepare-additional-components).

Jumping to `mydroid` directory
```bash
cd ${workspace}/mydroid
```
{: .dollar }


Please set Android build environment
```bash
export NUM_JOBS=$(($(nproc)*2))
source build/envsetup.sh
```
{: .dollar }


Please see more lunch build options at [Android build options](../application-notes/index.md#android-build-options)
```bash
lunch rzv2h_evk_ver1-ap4a-userdebug
```
{: .dollar }


Please set this variable to true for building Android bootloader
```bash
export BUILD_BOOTLOADERS=true
```
{: .dollar }


(**Mandatory to boot up**) Configure Mali graphics (See [Mali Graphics module](#mali-graphics-module-mandatory-to-boot-up))
```bash
vendor/arm/gralloc/configure
```
{: .dollar }


(**Mandatory if users want to use hardware codecs**) Enable hardware codecs (See [Hardware Codec module](#hardware-codec-module))
```bash
export ENABLE_HW_CODECS=true
```
{: .dollar }


(Optional) Support Encryption (See [Enable File-Based Encryption](../application-notes/index.md#enable-file-based-encryption))
```bash
export ENABLE_FBE=true
```
{: .dollar }


(Optional) Enable optional features (See [Enable optional features](../application-notes/index.md#enable-optional-features))

- Support USB Bluetooth
```bash
export ENABLE_BT_SUPPORT=true
```
{: .dollar }

- Support USB Wi-Fi (See [USB Wi-Fi module](#usb-wi-fi-module))
```bash
export USE_USB_WIFI=true
```
{: .dollar }


(Optional) Enable fastbootd for fastboot UDP (See [Fastboot UDP](../application-notes/index.md#fastboot-udp))
```bash
export USE_FASTBOOTD_FOR_UDP=true
```
{: .dollar }


(Optional) Enable MIPI Camera module support (See [MIPI Camera module](#mipi-camera-module))

Start building RZ AOSP
```bash
make -j${NUM_JOBS}
```
{: .dollar }

!!! danger "Caution"
	If the host PC is not powerful enough, please replace ${NUM_JOBS} by smaller build threads. For example: make -j4

Build finished. Please confirm this message

<span style="color:green">#### Build completed successfully (02:14:01 (hh\:mm\:ss)) ####</span>

Please set board name build. See more android build options at [Android build options](../application-notes/index.md#android-build-options). Default build option is ”Base”
```bash
export board_name=rzv2h_evk_ver1

# Please copy output files to <your_images_dir>
export images_dir=<your_images_dir>
cp out/target/product/${board_name}/init_boot.img                   ${images_dir}
cp out/target/product/${board_name}/boot.img                        ${images_dir}
cp out/target/product/${board_name}/vendor_boot.img                 ${images_dir}
cp out/target/product/${board_name}/dtb.img                         ${images_dir}
cp out/target/product/${board_name}/dtbo.img                        ${images_dir}
cp out/target/product/${board_name}/vbmeta.img                      ${images_dir}
cp out/target/product/${board_name}/super.img	                      ${images_dir}
cp out/target/product/${board_name}/codec_bin.img                   ${images_dir}
cp out/target/product/${board_name}/bl2_bp_rzv2h_evk_ver1_esd.srec  ${images_dir}
cp out/target/product/${board_name}/bl2_bp_rzv2h_evk_ver1_spi.srec  ${images_dir}
cp out/target/product/${board_name}/fip_rzv2h_evk_ver1_sdhi.srec    ${images_dir}
cp out/target/product/${board_name}/fip_rzv2h_evk_ver1_spi.srec     ${images_dir}
cp out/target/product/${board_name}/bl2_bp_rzv2h_evk_ver1_esd.bin   ${images_dir}
cp out/target/product/${board_name}/bl2_bp_rzv2h_evk_ver1_spi.bin   ${images_dir}
cp out/target/product/${board_name}/fip_rzv2h_evk_ver1_sdhi.bin     ${images_dir}
cp out/target/product/${board_name}/fip_rzv2h_evk_ver1_spi.bin      ${images_dir}
cp vendor/renesas/utils/fastboot/fastboot.sh                        ${images_dir}
cp vendor/renesas/utils/fastboot/fastboot_functions.sh              ${images_dir}
cp out/host/linux-x86/bin/adb                                       ${images_dir}
cp out/host/linux-x86/bin/mke2fs                                    ${images_dir}
cp out/host/linux-x86/bin/fastboot                                  ${images_dir}
chmod a+x -R ${images_dir}
	… Please read Note.
```
{: .dollar }


All \*.srec, \*.bin files are used for section [Flashing bootloader](../quick-start-guides/index.md#flashing-bootloader). All *.img files, fastboot.sh, and fastboot are used for section [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot).

<div style="border: 2px solid red; padding: 15px; margin-bottom: 30px">
<span style="color:red">Note: Please use “fastboot” (out/host/linux-x86/bin/) command that you built in this procedure. If you use old “fastboot” command which is included in old Android SDK, you might fail to flash an image.</span>
</div>
