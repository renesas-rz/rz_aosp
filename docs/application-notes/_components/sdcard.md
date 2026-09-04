## **SDCard storage support**

Due to pin multiplexing between the SDHI interface (used for SDCard storage) and the SDIO interface (used for Wi-Fi), both features cannot be enabled simultaneously.
To use SDCard functionality on the board, please configure the hardware switch and u-boot settings properly.

### **Hardware configuration**

1. Plug in SDCard to **SDIO Port**
2. Set **SW_OPT_MUX** switch to enable SDCard support:

<div class="table-no-sort" markdown="1">
| Switch Name | Pin1 | Pin2 | Pin3 | Pin4 |
| :-: | :-: | :-: | :-: | :-: |
| SW_OPT_MUX | OFF | - | - | - |
</div>

### **U-Boot configuration**

To enable SDCard storage support, set the required parameters in u-boot:

1. Power on the device and interrupt autoboot by pressing any key
2. Set the u-boot parameters:

    ```bash
    setenv use_usb_wifi 1
    saveenv
    ```
    {: .diamond2}

3. Reset the system:

    ```bash
    reset
    ```
    {: .diamond2}

!!! note
    Both hardware switch configuration and u-boot parameter settings are required for proper SDCard functionality.