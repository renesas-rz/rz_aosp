!!! warning "Notice"
	Please download `RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images.zip` package that includes the prebuilt images.

[:octicons-download-16: RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images.zip](https://www.renesas.com/document/sws/rzv2h-software-package-aosp-15-prebuilt-images){ .md-button .btn-round target=_blank }

To boot Android, it’s required to [flash Android bootloader](#flashing-bootloader) and [flash Android images](#flashing-images-using-fastboot).

Device connection information:

| Peripheral | RZ/V2H EVK |
| :--- | :--- |
| HDMI | HDMI (CN4) |
| USB cable for HDMI touch panel | USB 2.0 Type A Port (CN3) |
| USB cable for serial console | USB Micro-B Port (CN12) UART |
| USB cable for adb | USB Micro-B Port (CN2) |
| Ethernet cable | Ethernet port (CN6 and CN5) |

Start up the device by turning on switch POWER (SW3) and switch RESET(SW2).

<span style="color:red">**CAUTION:**</span> It's <span style="color:red">**NOT**</span> recommended to hot plug HDMI. It may cause board breaking.

<span style="color:red">**Note:**</span>

* It's required to disable "Auto Select" feature on monitor to disable auto scanning input.

The standard configuration is shown in the following figure.

<div style="float: right; width: 50%; text-align: center; margin-left: 20px;">
<img src="images/top_side_expansion.png" style="width: 90%;">
<em>Figure. Top side view of the RZ/V2H expansion board</em>
</div>

<div style="float: right; width: 50%; text-align: center; margin-left: 20px;">
<img src="images/top_side_main.png" style="width: 90%;">
<em>Figure. Top side view of the RZ/V2H EVK main board</em>
</div>

<table>
  <thead>
    <tr>
      <th style="text-align: center;">Number</th>
      <th style="text-align: left;">Description</th>
      <th style="text-align: center;">Board</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center;">1</td>
      <td>HDMI Port (CN4)</td>
      <td rowspan="5" style="vertical-align: middle; text-align: center; font-weight: bold;">Expansion</td>
    </tr>
    <tr><td style="text-align: center;">2</td><td>AUX port (P1)</td></tr>
    <tr><td style="text-align: center;">3</td><td>HP port (P2)</td></tr>
    <tr><td style="text-align: center;">4</td><td>Mic port (P3)</td></tr>
    <tr><td style="text-align: center;">5</td><td>MIPI DSI (CN5)</td></tr>

    <tr>
      <td style="text-align: center;">6</td>
      <td>Ethernet port (CN5)</td>
      <td rowspan="17" style="vertical-align: middle; text-align: center; font-weight: bold;">Main</td>
    </tr>
    <tr><td style="text-align: center;">7</td><td>Ethernet port (CN6)</td></tr>
    <tr><td style="text-align: center;">8</td><td>USB 2.0 Type-A (CN3)</td></tr>
    <tr><td style="text-align: center;">9</td><td>Micro USB 2.0 (CN2)</td></tr>
    <tr><td style="text-align: center;">10</td><td>USB 3.0 Type-A (CN4)</td></tr>
    <tr><td style="text-align: center;">11</td><td>SD card slot (SD1)</td></tr>
    <tr><td style="text-align: center;">12</td><td>SD card slot (SD2)</td></tr>
    <tr><td style="text-align: center;">13</td><td>UART USB debug serial (CN12)</td></tr>
    <tr><td style="text-align: center;">14</td><td>DSW1</td></tr>
    <tr><td style="text-align: center;">15</td><td>Power input (CN13)</td></tr>
    <tr><td style="text-align: center;">16</td><td>Power Switch (SW3)</td></tr>
    <tr><td style="text-align: center;">17</td><td>Reset Switch (SW2)</td></tr>
    <tr><td style="text-align: center;">18-21</td><td>MIPI-CSI (CN7-CN10)</td></tr>
    <tr><td style="text-align: center;">22</td><td>MIPI DSI (CN11)</td></tr>
  </tbody>
</table>

Connect the hardware as shown below.
<img src="images/hw_conf_v2h.png" style="width: 90%;">

## **Flashing bootloader**

It’s needed to update the firmware (*). Especially, it’s mandatory to use U-Boot which support “fastboot” command.

(*)bootloader binaries:

* bl2_bp_rzv2h_evk_ver1_esd.bin
* bl2_bp_rzv2h_evk_ver1_esd.srec
* bl2_bp_rzv2h_evk_ver1_spi.bin
* bl2_bp_rzv2h_evk_ver1_spi.srec
* fip_rzv2h_evk_ver1_sdhi.bin
* fip_rzv2h_evk_ver1_sdhi.srec
* fip_rzv2h_evk_ver1_spi.bin
* fip_rzv2h_evk_ver1_spi.srec.

Use provided *.mot (Flash Writer) firmware below for flashing SPI bootloader:

* Flash_Writer_SCIF_RZV2H_DEV_INTERNAL_MEMORY_0203.mot

Use provided *.ttl (TeraTerm Language) macros below for flashing SPI bootloader:

* V2H-EVK-1-IPL Macro-Flash Writer V0.60_921600bps_spi.ttl

Use provided script below for flashing eSD bootloader:

* flash_eSD_rzv2h_evk_ver1.sh

<span style="color:red">**Note:**</span>

* The command in the box below will be executed on the **Ubuntu Host PC**.
* In RZ/V2H EVK, SPI and eSD boot mode are supported.
* After first flashing new bootloaders of this release, the SPI bootloaders will be updated by default when users flash Android images. Please refer [Flashing images using fastboot](#flashing-images-using-fastboot) for more detail.

```bash
# For RZ/V2H prebuilt images
$ unzip RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images.zip

# Confirm the content of `RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images`
$ tree -L 1 RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images

# Content of the `RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images`
RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images
   |-- notice-files
   |-- prebuilt-images
   |-- sbom
   |-- L-497(Rev1.1)_RZ-MPU-ソフトウェアライセンス契約書.pdf
   |-- L-498(Rev1.1)_RZ-MPU-Software-License-Agreement.pdf
   `-- README.txt

# Confirm the content of prebuilt-images
$ tree RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images

# Content of the `RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images`
   |-- adb
   |-- bl2_bp_rzv2h_evk_ver1_esd.bin
   |-- bl2_bp_rzv2h_evk_ver1_esd.srec
   |-- bl2_bp_rzv2h_evk_ver1_spi.bin
   |-- bl2_bp_rzv2h_evk_ver1_spi.srec
   |-- boot.img
   |-- codec_bin.img
   |-- dtb.img
   |-- dtbo.img
   |-- fastboot
   |-- fastboot.sh
   |-- fastboot_functions.sh
   |-- fip_rzv2h_evk_ver1_sdhi.bin
   |-- fip_rzv2h_evk_ver1_sdhi.srec
   |-- fip_rzv2h_evk_ver1_spi.bin
   |-- fip_rzv2h_evk_ver1_spi.srec
   |-- init_boot.img
   |-- mke2fs
   |-- super.img
   |-- vbmeta.img
   |-- vendor_boot.img
   |-- flash_eSD_rzv2h_evk_ver1.sh
   |-- Flash_Writer_SCIF_RZV2H_DEV_INTERNAL_MEMORY_0203.mot
   `-- V2H-EVK-1-IPL Macro-Flash Writer V0.60_921600bps_spi.ttl
```

Please follow below steps to flash IPL (these steps are executed on Windows PC and use TeraTerm tool for flashing) on RZ/V2H boards.

<div class="page-break"></div>

### Method 1: Flash bootloaders by using SCIF Download Mode

1. Set DSW1 to SCIF Download Mode:

    |Switch Name|Pin1|Pin2|Pin3|Pin4|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|ON|OFF|ON|OFF|

    |Switch Name|Pin5|Pin6|Pin7|Pin8|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|ON|OFF|OFF|OFF|

2. Connect CN12 to Windows PC (via micro-USB cable), plug power adapter (<span style="color:red">**At least 100W**)</span> into Power Input (CN13). Run TeraTerm on Windows PC, choose correct COM port and change its Baud rate to 115200 (“Setup > Serial port…”).

3. On TeraTerm, choose “File > Disconnect” (if any), then “File > New connection…”. Turn switch POWER on (SW3), turn switch RESET on (SW2) to start up board and you will receive messages below:

    ```text
    SCI Download mode (Normal SCI boot)
    -- Load Program to SRAM -------------
    ```

4. Copy below files to the same folder on firmware Windows machine
    * All *.mot files
    * All *.ttl files
    * All “*.srec” files

    <span style="color:blue">**Note:**</span> Make sure to copy them to the same directory.

5. On TeraTerm, go to “Control > Macro”, choose corrected ttl file:<br>
    “V2H-EVK-1-IPL Macro-Flash Writer V0.60_921600bps_spi.ttl”<br>
    TeraTerm will automatically load firmware, then detect all **“*.srec”** files and load them to appropriate addresses.

    You will receive messages below after flashing bootloaders finished:

    ```text
    Please change to 115.2Kbps baud rate setting of the terminal.
    Changing to 115.2Kbps baud rate--------------DONE--------------
    ```

6. Turn off switch RESET (SW2), turn off switch POWER (SW3) and plug out Power input (CN13).

7. Set DSW1 to normal SPI boot mode:

    |Switch Name|Pin1|Pin2|Pin3|Pin4|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|ON|OFF|ON|OFF|

    |Switch Name|Pin5|Pin6|Pin7|Pin8|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|OFF|OFF|OFF|OFF|


8. Insert SD card (at least 16 GB) into SD1 slot.

    <span style="color:red">**Note:**</span> If no SD card is inserted, you will see error messages in the yellow box below:

    ```text
    Card did not respond to voltage select! : -110
    invalid mmc device
    Failed to read Android bootloader record
    ```

9. Plug in Power input (CN13) again. Turn on switch POWER (SW3) and switch RESET (SW2) again! On Teraterm choose “File > Disconnect”, “File > New connection…”. After this step, if you see the similar messages as yellow box below, it means that bootloader is loaded successfully.

    <span style="color:blue">**Expected SPI boot mode logs:**</span>
    ```text
    NOTICE: BL2: v2.7(release):v2.5/rzg2l-1.00-2305-gc3ed9fc4c
    NOTICE: BL2: Built : 20:52:34, Apr 21 2026
    NOTICE: BL2: Booting BL31
    NOTICE: BL31: v2.7(release):v2.5/rzg2l-1.00-2305-gc3ed9fc4c
    NOTICE: BL31: Built : 20:52:36, Apr 21 2026

    U-Boot 2021.10-gcc1de54513 (Apr 21 2026 - 20:48:06 +0700)

    CPU: Renesas Electronics R8A77970 rev 8.8
    Model: Renesas EVK Version 1 based on r9a09g057h4
    DRAM: 15.9 GiB
    WDT: watchdog@0000000014400000
    WDT: Started with servicing (60s timeout)
    MMC: mmc@15c00000: 0, mmc@15c10000: 1
    Loading Environment from SPIFlash... SF: Detected mt25qu512a with page size 256
    Bytes, erase size 64 KiB, total 64 MiB
    OK
    Saving Environment to SPIFlash... Erasing SPI flash...Writing to SPI flash...done
    OK
    In: serial@11c01400
    Out: serial@11c01400
    Err: serial@11c01400
    U-boot WDT started!
    Net:
    Error: ethernet@15c40000 address not set.

    Error: ethernet@15c30000 address not set.

    Error: ethernet@15c30000 address not set.

    Error: ethernet@15c40000 address not set.
    No ethernet found.

    Setting bootmode 'android'
    Hit any key to stop autoboot: 0
    ```

### Method 2: Flash bootloaders to eSD (eSD boot mode, see [Support eSD boot](../application-notes/index.md#support-esd-boot))

1. Plug SDCard into the host PC.

2. Copy the files below to the same folder on host PC:
    * bl2_bp_rzv2h_evk_ver1_esd.bin
    * fip_rzv2h_evk_ver1_sdhi.bin
    * flash_eSD_rzv2h_evk_ver1.sh

    ```bash
    # On Ubuntu Host PC, execute command:

    $ chmod a+x flash_eSD_rzv2h_evk_ver1.sh
    $ ./flash_eSD_rzv2h_evk_ver1.sh <block_dev_path_of_SDCard>

    Example: ./flash_eSD_rzv2h_evk_ver1.sh /dev/sdf (sdf is block device. It should not have partition number)
    Note: This script will format the SD card, so back up your data before proceeding
    ```

3. Set DSW1 to eSD boot mode:

    |Switch Name|Pin1|Pin2|Pin3|Pin4|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|ON|OFF|ON|ON|

    |Switch Name|Pin5|Pin6|Pin7|Pin8|
    | :-: | :-: | :-: | :-: | :-: |
    |DSW1|OFF|OFF|OFF|OFF|

4. Plug SDCard to SD1 on RZ/V2H EVK board, Turn on switch POWER (SW3) and switch RESET (SW2) to boot the board.

    <span style="color:red">**Note:**</span> Note: If the SD Card is not flashed eSD bootloaders yet or failed to flash eSD bootloaders, you will see error messages in the yellow box below:

    ```text
    SCI Download mode (Normal SCI boot)
    -- Load Program to SRAM -------------
    ```

    <span style="color:blue">**Expected eSD boot mode logs:**</span>
    ```text
    NOTICE: BL2: v2.7(release):v2.5/rzg2l-1.00-2305-gc3ed9fc4c
    NOTICE: BL2: Built : 13:14:36, Apr 23 2026
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x8136680 src=(p:0)0x60000(768) len=0x10(1)
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x8136850 src=(p:0)0x60010(768) len=0x28(1)
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x44000000 src=(p:0)0x60090(768) len=0x6071(49)
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x8136680 src=(p:0)0x60000(768) len=0x10(1)
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x8136850 src=(p:0)0x60010(768) len=0x28(1)
    NOTICE: Load dst=0x8136850 src=(p:0)0x60038(768) len=0x28(1)
    NOTICE: SD boot from partition 0
    NOTICE: Load dst=0x50000000 src=(p:0)0x66110(816) len=0xd2648(1684)
    NOTICE: BL2: Booting BL31
    NOTICE: BL31: v2.7(release):v2.5/rzg2l-1.00-2305-gc3ed9fc4c
    NOTICE: BL31: Built : 13:14:38, Apr 23 2026

    U-Boot 2021.10-gcc1de54513 (Apr 23 2026 - 13:14:28 +0700)

    CPU: Renesas Electronics CPU rev 1.0
    Model: Renesas EVK Version 1 based on r9a09g057h4
    DRAM: 15.9 GiB
    WDT: watchdog@0000000014400000
    WDT: Started with servicing (60s timeout)
    MMC: mmc@15c00000: 0, mmc@15c10000: 1
    Loading Environment from MMC... OK
    Saving Environment to MMC... Writing to MMC(0)... OK
    In: serial@11c01400
    Out: serial@11c01400
    Err: serial@11c01400
    U-boot WDT started!
    Net:
    Error: ethernet@15c40000 address not set.
    eth0: ethernet@15c30000
    Error: ethernet@15c40000 address not set.

    Setting bootmode 'android'
    Hit any key to stop autoboot: 0
    ```

<span style="color:red">**Note:**</span>

* This step is only for loading bootloaders. Users still need to flash Android images refer to [Flashing images using fastboot](#flashing-images-using-fastboot).
* After first flashing eSD bootloaders of this release, users do **NOT** need to use **flash_eSD_rzv2h_evk_ver1.sh** to update bootloaders. Users can use fastboot to update eSD bootloaders.

```bash
$ sudo ./fastboot.sh --serial=<serialno> --noresetenv --blonly --update_bootloaderesd
```
`<serialno>` is board serial number which is set in [Flashing images using fastboot](#flashing-images-using-fastboot).

