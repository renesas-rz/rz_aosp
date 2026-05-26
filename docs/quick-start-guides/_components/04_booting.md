## **Booting RZ/V2H EVK**

After flashing Bootloaders and images according to the [Quick Start Guides](../quick-start-guides/index.md), please follow the steps below to power on the RZ/V2H EVK.
>**Note**: This step expects the user to have completed the "flashing Bootloaders and images" of the [Quick Start Guides](../quick-start-guides/index.md)

1. Insert the microSD card to the Board.
2. Change DSW1 setting to SPI boot mode as shown above.
3. Connect Micro USB 2.0 (CN2) to Ubuntu Host PC with USB cable.
4. Connect the HDMI touch panel to the Board.
   >**Note**: HDMI monitor can also be used.
5. Connect the USB cable for HDMI touch panel to the USB 2.0 Type A (CN3).
   >**Note**: USB mouse can also be used.
6. Connect the USB camera via USB hub.
   >**Note**: Used when running YOLOv8 Application.
7. Connect the Windows PC and the Board by the Ethernet cable.
   >**Note**: Used when running YOLOv8 Streaming Application.
8. Connect the power cable to the board and turn SW3 ON.
9. Turn the SW2 to ON to power on the Board.
   Verify that the following is displayed on the HDMI screen.

    ![](images/boot_complete.png){width="100%"}

