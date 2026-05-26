## **Using SD Card boot**

Users can boot Android via SD card. Please follow the steps below to boot Android via SD card:

* Turn off the board. Insert SD card into SD2 slot.
* Power on board and interrupt at u-boot by pressing any key.
* Set boot devices (about mmc_dev, please refer table below):

<div class="table-no-sort" markdown="1">
| Board | Boot device | mmc_dev | soc_suffix | Default mode |
| :--- | :--- | :---: | :--- | :---: |
| RZ/V2H EVK | SDCard (SD1) | 0 | soc/15c00000.sd | ✓ |
| RZ/V2H EVK | SDCard (SD2) | 1 | soc/15c10000.sd |   |
</div>

* If SD card (on SD2 slot) does not contain an image, please flash new images by using fastboot (See [Flashing images using fastboot](../quick-start-guides/index.md#flashing-images-using-fastboot)).

<span style="color:red">**Note:**</span>

* No support external storage on SD1 slot when booting Android image by SD card on SD2 slot.
* The boot time depends on SDCard speed.
* It is required to turn off the board. Then unplug/plug Power Adapter to make sure SD card can be
initialized properly.
