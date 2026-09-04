## **Wi-Fi usage**

Due to pin multiplexing between the SDHI interface (used for SDCard storage) and the SDIO interface (used for Wi-Fi), both features cannot be enabled simultaneously. To use Wi-Fi functionality on the board, please configure the hardware switch and u-boot settings properly.

### **Hardware configuration**

1. Attach [2AE / 2BC M.2 Module](https://www.embeddedartists.com/products/2ae-m-2-module/) into **M2 Key B** slot

2. Set **SW_OPT_MUX** switch to enable Wi-Fi support:

    |Switch Name|Pin1|Pin2|Pin3|Pin4|
    | :-: | :-: | :-: | :-: | :-: |
    |SW_OPT_MUX|ON|-|-|-|

### **U-Boot configuration**

Make sure the `use_usb_wifi` variable is set to `0` in u-boot:

1. Power on the device and interrupt autoboot by pressing any key
2. Set the u-boot parameters:

    ```bash
    setenv use_usb_wifi 0
    saveenv
    ```
    {: .diamond2}

3. Reset the system:

    ```bash
    reset
    ```
    {: .diamond2}

!!! note
    Both hardware switch configuration and u-boot parameter settings are required for proper Wi-Fi functionality.
