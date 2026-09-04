## **Building Android, IPL, U-Boot, and Kernel sources**

!!! danger "CAUTION"
      It's required to download and extract additional components to build RZ AOSP.
      Please refer [Prepare additional components](#prepare-additional-components)

### *How to build IPL, U-boot by script*

Jumping to `mydroid` directory
```bash
cd ${workspace}/mydroid
```
{: .dollar }

Please use below command for building Android bootloader
```bash
./vendor/renesas/utils/bootloaders/build_bootloader.sh SMARC_RZG3L
```
{: .dollar }

Build finished. Please confirm this message

```bash
====================================================
Artifacts for device SMARC_RZG3L
   ... Bootloader Binary List
```

Please confirm the output

```bash
tree -L 1 vendor/renesas/utils/bootloaders/smarc_rzg3l_out/
```
{: .dollar }

```text
vendor/renesas/utils/bootloaders/smarc_rzg3l_out/
├── bl2_bp_emmc.bin
├── bl2_bp_emmc.srec
├── bl2_bp_esd.bin
├── bl2_bp_esd.srec
├── bl2_bp_smarc_rzg3l_emmc.bin
├── bl2_bp_smarc_rzg3l_emmc.srec
├── bl2_bp_smarc_rzg3l_esd.bin
├── bl2_bp_smarc_rzg3l_esd.srec
├── bl2_bp_smarc_rzg3l_spi.bin
├── bl2_bp_smarc_rzg3l_spi.srec
├── bl2_bp_spi.bin
├── bl2_bp_spi.srec
├── bp_emmc.bin
├── bp_esd.bin
├── bp_spi.bin
├── fip.bin
├── fip_smarc_rzg3l.bin
├── fip_smarc_rzg3l.srec
├── fip.srec
├── host_tools.log
├── ipl.log
├── obj
├── u-boot.bin
└── u-boot.log
```

### *Building Android and Kernel sources*

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
lunch smarc_rzg3l-cp2a-userdebug
```
{: .dollar }

(**Mandatory if users want to use hardware codecs**) Enable hardware codecs (See [Hardware Codec module](#hardware-codec-module))
```bash
export ENABLE_HW_CODECS=true
```
{: .dollar }

(Optional) Enable Wi-Fi support (See [Extract Wi-Fi firmware](#extract-wi-fi-firmware))
```bash
export ENABLE_WIFI_SUPPORT=true
```
{: .dollar }

Start building RZ AOSP
```bash
make -j${NUM_JOBS}
```
{: .dollar }

!!! danger "CAUTION"
      If the host PC is not powerful enough, please replace `${NUM_JOBS}` by smaller build threads. For example: `make -j4`

Build finished. Please confirm this message

<span style="color:green">#### Build completed successfully (02:14:01 (hh\:mm\:ss)) ####</span>

Please set board name build. See more android build options at [Android build options](../application-notes/index.md#android-build-options). Default build option is ”Base”
```bash
export board_name=smarc_rzg3l

# Please copy output files to <your_images_dir>
export images_dir=<your_images_dir>
cp out/target/product/${board_name}/init_boot.img                                   ${images_dir}
cp out/target/product/${board_name}/boot.img                                        ${images_dir}
cp out/target/product/${board_name}/vendor_boot.img                                 ${images_dir}
cp out/target/product/${board_name}/dtb.img                                         ${images_dir}
cp out/target/product/${board_name}/dtbo.img                                        ${images_dir}
cp out/target/product/${board_name}/vbmeta.img                                      ${images_dir}
cp out/target/product/${board_name}/super.img	                                      ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/bl2_bp_smarc_rzg3l_emmc.srec  ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/bl2_bp_smarc_rzg3l_emmc.bin   ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/bl2_bp_smarc_rzg3l_esd.srec   ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/bl2_bp_smarc_rzg3l_esd.bin    ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/fip_smarc_rzg3l.srec          ${images_dir}
cp vendor/renesas/utils/bootloaders/${board_name}_out/fip_smarc_rzg3l.bin           ${images_dir}
cp vendor/renesas/utils/fastboot/fastboot.sh                                        ${images_dir}
cp vendor/renesas/utils/fastboot/fastboot_functions.sh                              ${images_dir}
cp out/host/linux-x86/bin/adb                                                       ${images_dir}
cp out/host/linux-x86/bin/mke2fs                                                    ${images_dir}
cp out/host/linux-x86/bin/fastboot                                                  ${images_dir}
chmod a+x -R ${images_dir}
	… Please read Note.
```
{: .dollar }

All \*.srec, \*.bin files are used for section [Flashing bootloader](../quick-start-guides/index.md#flashing-bootloader). All *.img files, fastboot.sh, and fastboot are used for section [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot).

!!! note
      Please use `fastboot` (out/host/linux-x86/bin/) command that you built in this procedure. If you use old `fastboot` command which is included in old Android SDK, you might fail to flash an image.
