## **Flashing images using fastboot**

This step should be done after successful IPL and U-Boot flashing. (See [Flashing bootloader](#flashing-bootloader))

<span style="color:red">**Note:**</span> When users load bootloader at the first time, bootloaders will display warning messages as below:

```text
    cannot find partition: 'misc'
    Failed to read Android bootloader record.
```

**This warning is expected**. The "misc" partition doesn't exist yet because no Android images have been flashed. It will be created automatically during the Android image flashing steps.

1) There are 2 ways to flash images:

- In case using “fastboot usb” please connect Micro USB 2.0 (CN2) to Ubuntu Host PC with an USB cable for fastboot.
- In case using “fastboot udp” please connect Ethernet port (CN5) via Ethernet cable to a router and an Ubuntu Host PC connected to the same router.

2) Power on device and interrupt autoboot. <br>
3) Execute below commands on target board.

  Set environment values on U-boot
```bash
=> env default -a
=> setenv bootargs ‘video=HDMI-A-1:e $bootargs’
	video=HDMI-A-1:e : Skip hotplug, keep connector always on
```

  For fastboot USB
```bash
# For fastboot USB
=> setenv serialno <serial number>
	Example:
	setenv serialno 00001234
=> saveenv
=> fastboot usb
```
  For fastboot UDP (see [Fastboot UDP](../application-notes/index.md#fastboot-udp))
```bash
=> setenv ethaddr <board MAC addr>
=> setenv ipaddr <board IP addr>
=> setenv bootargs ‘ip=<client-ip>::<gateway-ip>:<netmask>::<device>:off $bootargs’
	<client-ip>: Board IP address
	<gateway-ip>: Host PC IP address
	<netmask>: Network mask
	<device>: Network interface
	Example:
	setenv ethaddr aa:bb:cc:dd:ee:ff
	setenv ipaddr 192.168.1.2
	setenv bootargs 'ip=192.168.1.2::192.168.1.1:255.255.255.0::eth0:off $bootargs'
=> saveenv
=> fastboot udp
```

<span style="color:red">**Note:**</span>

* fastboot device is only detected if user runs fastboot usb command on u-boot console.
* If the “**ip**” is set in **bootargs** and the Ethernet cable is not plugged in, the system will wait for 100 seconds during boot

4) Execute below commands on Ubuntu Host PC.

Format SD card partition and write image file to target. Please use “fastboot” command that you built in step [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources). (Of course, fastboot tool included in latest Android SDK is also worked.)

### Method 1: Fastboot USB

```bash
$ cd <your working dir>/RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images
$ chmod a+x *

$ sudo ./fastboot -s <serialno> oem format
Expected output: "Finished. Total time: 1.857s"

$ sudo ./fastboot -s <serialno> reboot bootloader
Expected output: "Finished. Total time: 0.266s"

# In case of SPI boot, fastboot.sh updates Android images and SPI bootloaders
$ sudo ./fastboot.sh --serial=<serialno> --noresetenv

# In case of eSD boot, fastboot.sh updates Android images and eSD bootloaders
$ sudo ./fastboot.sh --serial=<serialno> --noresetenv --update_bootloaderesd

# If users do not want to update bootloaders
$ sudo ./fastboot.sh --serial=<serialno> --noresetenv --nobl

Expected output: "SUCCESS. Script finished successfully"

Additional option:
	--blonly: Update bootloaders only

<serialno> is board serial number which is set in the board console.
```

### Method 2: Fastboot UDP (See [Fastboot UDP](../application-notes/index.md#fastboot-udp))

For SPI Flash only (not supported eSD boot mode)

```bash
$ cd <your working dir>/RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images
$ chmod a+x *

$ sudo ./fastboot -s udp:<ipaddress> oem format
Expected output: "Finished. Total time: 1.652s"

$ sudo ./fastboot -s udp:<ipaddress> reboot bootloader
Expected output: "Finished. Total time: 0.013s"

$ sudo ./fastboot.sh --serial=udp:<ipaddress> --noresetenv --nobl
Expected output: "SUCCESS. Script finished successfully"

<ipaddress> is board IP address which is set in the board console.
# Fastboot UDP only work on Ethernet port (CN5).
```

<span style="color:red">**Note:**</span>

- Running **oem format** may be failed at the first time. The information might be like the log below.
    ```text
    (bootloader)  eMMC: Man 000003 Snr 290cbd00 SE16G 0.1 15193MiB
    (bootloader)  Created new GPT partition table:
    (bootloader)      /misc (ERROR unable to get info)
    (bootloader)      /pst (ERROR unable to get info)
    (bootloader)      /vbmeta (ERROR unable to get info)
    (bootloader)      /vbmeta (ERROR unable to get info)
    (bootloader)      /dtbo (ERROR unable to get info)
    (bootloader)      /dtbo (ERROR unable to get info)
    (bootloader)      /boot (ERROR unable to get info)
    (bootloader)      /boot (ERROR unable to get info)
    (bootloader)      /init_boot (ERROR unable to get info)
    (bootloader)      /init_boot (ERROR unable to get info)
    (bootloader)      /codec_bin_a (ERROR unable to get info)
    (bootloader)      /codec_bin_b (ERROR unable to get info)
    (bootloader)      /vendor_boot (ERROR unable to get info)
    (bootloader)      /vendor_boot (ERROR unable to get info)
    (bootloader)      /metadata (ERROR unable to get info)
    (bootloader)      /super (ERROR unable to get info)
    (bootloader)      /userdata (ERROR unable to get info)
    OKAY [  1.956s]
    Finished. Total time: 1.957s
    ```

Please try to turn off your board, plug out power. Then plug in power, turn on the board again and try to re-run **oem format** again

- HDMI is required to boot successfully.
- It is required to plug external power if user uses external devices like portable monitor, USB hub, etc.

Once the boot process completes successfully, the GUI should appear on the HDMI monitor.

<p align="center">
  <img src="images/boot_complete.png" alt="Boot complete" width="100%">
</p>

The console should display logs like the following:
```text
[ 140.089754] init: Command 'setprop persist.device_config.attempted_boot_count 0' action=sys.boot_completed=1 (/system/etc/init/flags_health_check.rc:8) took 60ms and succeeded
```
