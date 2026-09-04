## **Using SDCard boot**

Due to pin multiplexing between the SDHI interface (used for SDCard boot) and the SDIO interface (used for Wi-Fi), both features cannot be enabled simultaneously.
To use SDCard boot functionality on the board, please configure the hardware switch and u-boot settings properly.

### **Hardware configuration**

1. Plug in SDCard to **SDIO Port**
2. Set **SW_OPT_MUX** switch to enable SDCard support:

<div class="table-no-sort" markdown="1">
| Switch Name | Pin1 | Pin2 | Pin3 | Pin4 |
| :-: | :-: | :-: | :-: | :-: |
| SW_OPT_MUX | OFF | - | - | - |
</div>

### **U-Boot configuration**

To enable SDCard boot support, set the required parameters in u-boot:

1. Power on the device and interrupt autoboot by pressing any key
2. Set the u-boot parameters:

    ```bash
    setenv boot_device 1
    setenv use_usb_wifi 1
    saveenv
    ```
    {: .diamond2}

3. Press and hold the Power button (POWER) for 2 seconds to turn off board. Press and hold the Power button (POWER) for 2 seconds to turn on board again!

4. Interrupt autoboot by pressing any key and Flash Android image. Please follow [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot)

!!! note 
    * Set boot devices (about mmc_dev, please refer table below):

<div class="table-no-sort">
<table>
<thead>
<tr>
<th style="text-align: left">Board</th>
<th style="text-align: left">Boot device</th>
<th style="text-align: center">mmc_dev</th>
<th style="text-align: left">soc_suffix</th>
<th style="text-align: center">Default mode</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="2" style="text-align: left; vertical-align: middle;">SMARC RZ/G3L</td>
<td style="text-align: left">eMMC/SDCard (uSD0) for eSD boot</td>
<td style="text-align: center">0</td>
<td style="text-align: left">soc/11c00000.mmc</td>
<td style="text-align: center">✓</td>
</tr>
<tr>
<td style="text-align: left">SDCard</td>
<td style="text-align: center">1</td>
<td style="text-align: left">soc/11c10000.mmc</td>
<td style="text-align: center"></td>
</tr>
</tbody>
</table>
</div>


!!! note
    * Both hardware switch configuration and u-boot parameter settings are required for proper SDCard boot functionality.
    * The boot time depends on SDCard speed.

