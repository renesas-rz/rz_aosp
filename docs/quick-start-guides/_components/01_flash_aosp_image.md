!!! warning "Notice"
	Please download `RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images.zip` package that includes the prebuilt images.

[:octicons-download-16: RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images.zip](https://www.renesas.com/document/sws/rzg3l-software-package-aosp-17-prebuilt-images){ .md-button .btn-round target=_blank }

To boot Android, it’s required to [flash Android bootloader](#flashing-bootloader) and [flash Android images](#flashing-images-using-fastboot).

Device connection information:

| Peripheral | SMARC RZ/G3L |
| :--- | :--- |
| HDMI | Mirco HDMI (HDMI)  |
| USB cable for HDMI touch panel | USB 2.0 Type A Port (USB1B-1A_HOST) |
| USB cable for serial console | USB debug serial (SER3_UART) |
| USB cable for adb | Micro USB 2.0 (USB0_OTG)  |
| Ethernet cable | Ethernet port 0 (ETH0), Ethernet port 1 (ETH1)  |

Start up the device by pressing and hold the Power button (POWER) for 2 seconds. 

!!! danger "Caution"
    It's <span style="color:red">**NOT**</span> recommended to hot plug HDMI. It may cause board broken.

!!! note
    * It's required to disable "Auto Select" feature on monitor to disable auto scanning input.

The standard configuration is shown in the following figure.

<div style="float: right; width: 50%; text-align: center; margin-left: 20px;">
<img src="images/bottom_side.png" style="width: 90%;">
<em>Figure. Bottom side view of the SMARC RZ/G3L main board</em>
</div>

<div style="float: right; width: 50%; text-align: center; margin-left: 20px;">
<img src="images/top_side_main.png" style="width: 90%;">
<em>Figure. Top side view of the SMARC RZ/G3L main board</em>
</div>

<table>
  <thead>
    <tr>
      <th style="text-align: center;">Number</th>
      <th style="text-align: left;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">1</td>
      <td>Power input (USB-C_PWR_IN)</td>
    </tr>
    <tr><td style="text-align: center;">2</td><td>Power button (POWER)</td></tr>
    <tr><td style="text-align: center;">3</td><td>Reset button (RESET)</td></tr>
    <tr><td style="text-align: center;">4</td><td>Sleep button (SLEEP)</td></tr>
    <tr><td style="text-align: center;">5</td><td>USB debug serial (SER3_UART)</td></tr>
    <tr><td style="text-align: center;">6</td><td>Micro USB 2.0 (USB0_OTG)</td></tr>
    <tr><td style="text-align: center;">7</td><td>USB 2.0 Type-A (USB1B-1A_HOST)</td></tr>
    <tr><td style="text-align: center;">8</td><td>Ethernet port (ETH1) and (ETH0)</td></tr>
    <tr><td style="text-align: center;">9</td><td>MIPI-CSI2 connector (CAM_CSI1)</td></tr>
    <tr><td style="text-align: center;">10</td><td>Android POWER Button</td></tr>
    <tr><td style="text-align: center;">11</td><td>Volume Down Button</td></tr>
    <tr><td style="text-align: center;">12</td><td>Volume Up Button</td></tr>
    <tr><td style="text-align: center;">13</td><td>AUX/Headphone/MIC connector (AUDIO)</td></tr>
    <tr><td style="text-align: center;">14</td><td>Micro SDCard slot (SDI0)</td></tr>
    <tr><td style="text-align: center;">15</td><td>BOOT MODE (SW_MODE)</td></tr>
    <tr><td style="text-align: center;">16</td><td>SW_OPT_MUX</td></tr>
    <tr><td style="text-align: center;">17</td><td>eSD (uSD0)</td></tr>
    <tr><td style="text-align: center;">18</td><td>LED (DDR_RET)</td></tr>
    <tr><td style="text-align: center;">19</td><td>RZ SMARC Breakout (CN1)</td></tr>
    <tr><td style="text-align: center;">20</td><td>Micro HDMI (HDMI)</td></tr>
    <tr><td style="text-align: center;">21</td><td>Wi-Fi (2AE / 2BC M.2 Module)</td></tr>
  </tbody>
</table>

## **Flashing AOSP image**
### **Flashing bootloader**

It’s needed to update the firmware (*). Especially, it’s mandatory to use U-Boot which support “fastboot” command.

(*)bootloader binaries:

* bl2_bp_smarc_rzg3l_emmc.bin
* bl2_bp_smarc_rzg3l_emmc.srec
* bl2_bp_smarc_rzg3l_esd.bin
* bl2_bp_smarc_rzg3l_esd.srec
* fip_smarc_rzg3l.bin
* fip_smarc_rzg3l.srec

Use provided *.mot (Flash Writer) firmware below for flashing eMMC bootloader:

* Flash_Writer_SCIF_RZG3L_SMARC_LPDDR4.mot

Use provided *.ttl (TeraTerm Language) macros below for flashing eMMC bootloader:

* emmc_flash_rzg3l.ttl

Use provided script below for flashing eSD bootloader:

* flash_eSD_smarc_rzg3l.sh

!!! note
    * The command in the box below will be executed on the **Ubuntu Host PC**.
    * In SMARC RZ/G3L, eMMC and eSD boot mode are supported.

* For RZ/G3L prebuilt images

```bash
unzip RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images.zip
```
{: .dollar }

* Confirm the content of `RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images`

```bash
tree -L 1 RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images
```
{: .dollar }

* Content of the `RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images`
```text
RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images
├── L-497(Rev1.1)_RZ-MPU-Video-Codecパッケージ_利用許諾契約書_RZG3L-AOSP-17.pdf
├── L-498(Rev1.1)_Video-Codec-Package-for-RZ-MPU_Software-License-Agreement_RZG3L-AOSP-17.pdf
├── notice-files
├── prebuilt-images
├── README.txt
└── sbom
```

* Confirm the content of prebuilt-images
```bash
tree RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images/prebuilt-images
```
{: .dollar }


* Content of the `RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images/prebuilt-images`
```text
   |-- adb
   |-- bl2_bp_smarc_rzg3l_emmc.bin
   |-- bl2_bp_smarc_rzg3l_emmc.srec
   |-- bl2_bp_smarc_rzg3l_esd.bin
   |-- bl2_bp_smarc_rzg3l_esd.srec
   |-- boot.img
   |-- dtb.img
   |-- dtbo.img
   |-- fastboot
   |-- fastboot.sh
   |-- fastboot_functions.sh
   |-- fip_smarc_rzg3l.bin
   |-- fip_smarc_rzg3l.srec
   |-- init_boot.img
   |-- mke2fs
   |-- super.img
   |-- vbmeta.img
   |-- vendor_boot.img
   |-- flash_eSD_smarc_rzg3l.sh
   |-- Flash_Writer_SCIF_RZG3L_SMARC_LPDDR4.mot
   `-- emmc_flash_rzg3l.ttl
```

Please follow the steps below to flash IPL (these steps are executed on Windows PC and use TeraTerm 
tool for flashing) on RZ/G3L boards. 

<div class="page-break"></div>

=== "Method 1:  Flash bootloaders to eMMC (eMMC boot mode)"

    1. Set SW_MODE to SCIF Download Mode:

        |Switch Name|Pin1|Pin2|Pin3|Pin4|
        | :-: | :-: | :-: | :-: | :-: |
        |SW_MODE|OFF|ON|OFF|ON|

    2.  Connect SER3_UART to Windows PC (via micro-USB cable), plug power adapter into Power 
    Input (POWER). Run TeraTerm on Windows PC, choose correct COM port and change its Baud rate 
    to 115200 (“Setup > Serial port...”). 

    3.  On TeraTerm, choose “File > Disconnect” (if any), then “File > New connection…”. Press and hold 
    the Power button (POWER) for 2 seconds to start up board and you will receive messages below: 

        ```text
        SCI Download mode (Normal SCI boot)
        -- Load Program to SRAM -------------
        ```

    4. Copy below files to the same folder on firmware Windows machine
        * All “*.mot” files
        * All “*.ttl” files
        * All “*.srec” files

        !!! note
            Make sure to copy them to the same directory.

    5. On TeraTerm, go to “Control > Macro”, choose corrected ttl file:<br>
        “emmc_flash_rzg3l.ttl”<br>
        TeraTerm will automatically load firmware, then detect all **“*.srec”** files and load them to appropriate addresses.

    6. After loading finished, the output looks like:

        ```text
        SAVE -FLASH....... 
        EM_W Complete! 
        >
        ```

    7. Press and hold the Power button (POWER) for 2 seconds to turn off board
    and plug out Power input

    8. Set SW_MODE to eMMC boot mode:

        |Switch Name|Pin1|Pin2|Pin3|Pin4|
        | :-: | :-: | :-: | :-: | :-: |
        |SW_MODE|ON|OFF|OFF|ON|

    9. Plug in Power input again. Press and hold the Power button (POWER) for 2 seconds to turn on
    board again! On Teraterm choose “File > Disconnect”, “File > New connection…”. After this step, if 
    you see the similar messages as yellow box below, it means that bootloader is loaded successfully.

        ```text
        NOTICE:  BL2: v2.10.5(release):ed630410f
        NOTICE:  BL2: Built : 10:28:43, Aug 10 2026
        NOTICE:  eMMC boot from partition 1
        NOTICE:  BL2: SYS_LSI_MODE: 0x13051
        NOTICE:  BL2: SYS_LSI_DEVID: 0x87d9447
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x42540 src=(p:1)0x60000(768) len=0x10(1)
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x426d8 src=(p:1)0x60010(768) len=0x28(1)
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x44000000 src=(p:1)0x60090(768) len=0x3e000(497)
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x42540 src=(p:1)0x60000(768) len=0x10(1)
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x426d8 src=(p:1)0x60010(768) len=0x28(1)
        NOTICE:  Load dst=0x426d8 src=(p:1)0x60038(768) len=0x28(1)
        NOTICE:  eMMC boot from partition 1
        NOTICE:  Load dst=0x50000000 src=(p:1)0x9e090(1264) len=0xd5440(1707)
        NOTICE:  BL2: Booting BL31
        NOTICE:  BL31: v2.10.5(release):ed630410f
        NOTICE:  BL31: Built : 10:28:46, Aug 10 2026


        U-Boot 2024.07-gabd6dbbbe3 (Aug 10 2026 - 10:28:33 +0700)

        CPU:   Renesas Electronics CPU rev 16.15
        Model: smarc-rzg3l
        DRAM:  1.9 GiB
        Core:  28 devices, 16 uclasses, devicetree: separate
        MMC:   sd@11c00000: 0, sd@11c10000: 1
        Loading Environment from MMC... Reading from MMC(0)... OK
        In:    serial@100ac000
        Out:   serial@100ac000
        Err:   serial@100ac000
        Net:
        Error: ethernet@11c40000 No valid MAC address found.

        Error: ethernet@11c30000 No valid MAC address found.

        Error: ethernet@11c30000 No valid MAC address found.

        Error: ethernet@11c40000 No valid MAC address found.
        No ethernet found.

        Hit any key to stop autoboot:  0
        ```
        
    !!! danger "CAUTION"
        * This step is only for loading bootloaders. Users still need to flash Android images to boot Android. 

    !!! note
        * After first flashing eMMC bootloaders of this release, users can use fastboot to update eMMC bootloaders. 
        * U-boot environment variables will be erased after updating bootloaders by fastboot (fastboot.sh). Please back up before updating.

    !!! note
        To run update eMMC bootloaders properly, It's required to set 'platform' variable to r9a08g046 via command in u-boot console
    
        ```bash
        setenv platform r9a08g046
        saveenv
        ```
        {: .diamond2 }

    * To be in fastboot mode, please execute below command in u-boot console:

    ```bash
    run fastbootcmd
    ```
    {: .diamond2 }

    *  On Ubuntu host PC, execute command:

    ```bash
    sudo ./fastboot.sh --serial=<serial#> --noresetenv --blonly --update_bootloaderemmc
    ```
    {: .dollar }

    `<serial#>` is board serial number which is set in [Flashing images using fastboot](#flashing-images-using-fastboot).

=== "Method 2: Flash bootloaders to eSD (eSD boot mode, see [Support eSD boot](../application-notes/index.md#support-esd-boot))"

    1. Plug SDCard into the host PC.

    2. Copy the files below to the same folder on host PC:
        * bl2_bp_smarc_rzg3l_esd.bin
        * fip_smarc_rzg3l.bin
        * flash_eSD_smarc_rzg3l.sh

        * On Ubuntu Host PC, execute command:

        ```bash
        chmod a+x flash_eSD_smarc_rzg3l.sh
        ./flash_eSD_smarc_rzg3l.sh <block_dev_path_of_SDCard>
        ```
        {: .dollar}

        ```text
        Example: ./flash_eSD_smarc_rzg3l.sh/dev/sdf (sdf is block device. It should not have partition number)
        ```

        !!! danger "CAUTION"
            This script will format the SD card, so back up your data before proceeding

    3. Set SW_MODE to eSD boot mode:

        |Switch Name|Pin1|Pin2|Pin3|Pin4|
        | :-: | :-: | :-: | :-: | :-: |
        |SW_MODE|ON|ON|OFF|ON|

    4. Plug SDCard to uSD0 on RZ/G3L SMARC SOM board, press Reset button (RESET) to boot the 
    board 

        <span style="color:blue">**Expected eSD boot mode logs:**</span>
        ```text
        NOTICE:  BL2: v2.10.5(release):ed630410f
        NOTICE:  BL2: Built : 08:47:57, Aug  5 2026
        NOTICE:  SD boot from partition 0
        NOTICE:  BL2: SYS_LSI_MODE: 0x13001
        NOTICE:  BL2: SYS_LSI_DEVID: 0x87d9447
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x42540 src=(p:0)0x60000(768) len=0x10(1)
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x426d8 src=(p:0)0x60010(768) len=0x28(1)
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x44000000 src=(p:0)0x60090(768) len=0x3e000(497)
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x42540 src=(p:0)0x60000(768) len=0x10(1)
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x426d8 src=(p:0)0x60010(768) len=0x28(1)
        NOTICE:  Load dst=0x426d8 src=(p:0)0x60038(768) len=0x28(1)
        NOTICE:  SD boot from partition 0
        NOTICE:  Load dst=0x50000000 src=(p:0)0x9e090(1264) len=0xd5440(1707)
        NOTICE:  BL2: Booting BL31
        NOTICE:  BL31: v2.10.5(release):ed630410f
        NOTICE:  BL31: Built : 08:48:01, Aug  5 2026


        U-Boot 2024.07-gabd6dbbbe3 (Aug 05 2026 - 08:46:59 +0700)

        CPU:   Renesas Electronics CPU rev 16.13
        Model: smarc-rzg3l
        DRAM:  1.9 GiB
        Core:  28 devices, 16 uclasses, devicetree: separate
        MMC:   sd@11c00000: 0, sd@11c10000: 1
        Loading Environment from MMC... Reading from MMC(0)... *** Warning - bad CRC, using default environment

        Use boot device: mmc 0 (eMMC/eSD)
        himport_r: can't insert "boot_device=-1" into hash table
        Use boot device: mmc 0 (eMMC/eSD)
        In:    serial@100ac000
        Out:   serial@100ac000
        Err:   serial@100ac000
        Net:
        Error: ethernet@11c40000 No valid MAC address found.

        Error: ethernet@11c30000 No valid MAC address found.

        Error: ethernet@11c30000 No valid MAC address found.

        Error: ethernet@11c40000 No valid MAC address found.
        No ethernet found.

        Hit any key to stop autoboot:  0
        ```

    !!! danger "CAUTION"
        * This step is only for loading bootloaders. Users still need to flash Android images refer to [Flashing images using fastboot](#flashing-images-using-fastboot).

    !!! note
        * After first flashing eSD bootloaders of this release, users do **NOT** need to use **flash_eSD_smarc_rzg3l.sh** to update bootloaders. Users can use fastboot to update eSD bootloaders.
        * U-boot environment variables will be erased after updating bootloaders by fastboot (fastboot.sh). Please back up before updating.

    !!! note
        To run update eSD bootloaders properly, It's required to set 'platform' variable to r9a08g046 via command in u-boot console
    
        ```bash
        setenv platform r9a08g046
        saveenv
        ```
        {: .diamond2 }

    * To be in fastboot mode, please execute below command in u-boot console:

    ```bash
    run fastbootcmd
    ```
    {: .diamond2 }

    *  On Ubuntu host PC, execute command:

    ```bash
    sudo ./fastboot.sh --serial=<serial#> --noresetenv --blonly --update_bootloaderesd
    ```
    {: .dollar }

    `<serial#>` is board serial number which is set in [Flashing images using fastboot](#flashing-images-using-fastboot).

### **Flashing images using fastboot**

This step should be done after successful IPL and U-Boot flashing. (See [Flashing bootloader](#flashing-bootloader))

!!! note
    When users load bootloader at the first time, bootloaders will display warning messages as below:

```text
Could not find "misc" partition
```

**This warning is expected**. The "misc" partition doesn't exist yet because no Android images have been flashed. It will be created automatically during the Android image flashing steps.

1) Using “fastboot usb”, please connect USB0_OTG to Ubuntu Host PC with an USB 
cable for fastboot. <br>
2) Power on device and interrupt autoboot. <br>
3) Execute below commands on target board.

  Set environment values on U-boot

```bash
env default -a 
setenv serial# <serial number>  # Set board serial number to serial#: 0000XXXX (where XXXX = board number like 0011) 
editenv bootargs
```
{: .diamond2} 

```bash
Edit bootargs: video=XXXX-X:d 
“video” variable needs to set parameter related to display configuration. 
video=HDMI-A-1:e (Skip hotplug, keep connector always on)
```
{: .hash} 

```bash
saveenv 
reset  # Please Interrupt autoboot 
run fastbootcmd
```
{: .diamond2} 

4) Execute below commands on Ubuntu Host PC.

Format eMMC/SD card partition and write image file to target. Please use “fastboot” command that you built in step [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources). (Of course, fastboot tool included in latest Android SDK is also worked.)

#### **Method: Fastboot USB**

* Following below commands to flash Android images:

```bash
cd <your working dir>/RTK0EF0188Z78001ZJ_v17.0.0_prebuilt-images/prebuilt-images
chmod a+x *
sudo ./fastboot -s <serial#> oem format # Expected output: "Finished. Total time: x.xxxs"
sudo ./fastboot -s <serial#> reboot bootloader # Expected output: "Finished. Total time: x.xxxs"
sudo ./fastboot.sh --serial=<serial#> --noresetenv --nobl # Expected output: "SUCCESS. Script finished successfully"
```
{: .dollar }

!!! note
    * HDMI is required to boot successfully.
    * It is required to plug external power if user uses external devices like portable monitor, USB hub, etc.

Once the boot process completes successfully, the GUI should appear on the HDMI monitor.

<p align="center">
  <img src="images/boot_complete.png" alt="Boot complete" width="100%">
</p>

The console should display logs like the following:
```text
[   50.869220] init: processing action (sys.boot_completed=1) from (/system/etc/init/hw/init.rc:1237)
```


