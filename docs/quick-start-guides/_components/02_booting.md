## **Booting SMARC RZ/G3L**

!!! note
      To boot the Android on RZ/G3L, it's required to flash Bootloaders and flash Android images according to  the [Quick Start Guides](../quick-start-guides/index.md)

Please follow below steps to boot Android on SMARC RZ/G3L:

1. Change SW_MODE setting to [eMMC boot mode](#__tabbed_1_1).
2. Connect Micro USB 2.0 (USB0_OTG) to Ubuntu Host PC with USB cable.
3. Connect the HDMI touch panel to the Board.
   >**Note**: HDMI monitor can also be used.
4. Connect the USB cable for HDMI touch panel to the USB 2.0 Type A (USB1B-1A_HOST).
   >**Note**: USB mouse can also be used.
5. Connect the power cable to the board, press and hold the Power button (POWER) for 2 seconds. <br>
   Verify that the following is displayed on the HDMI screen.

    ![](images/boot_complete.png){width="100%"}

!!! Note
    * Devices with #AC0 or #BC0 in the part number, as well as RZ/G3L EVKIT with Lot # 0000308367 –0000309059 that incorporate these devices, have limitations in the MIPI DSI feature.
    * For details, please contact a Renesas Electronics sales representative.


