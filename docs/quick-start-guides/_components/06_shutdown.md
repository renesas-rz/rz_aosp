## **Shutdown device**

Shutdown the device as shown:

### Method 1: Shutdown via board's console

On board's console:

> 1)  $ reboot -p

> 2)  Switch the RESET switch (SW2) and POWER switch (SW3) off after the display shows no signal

### Method 2: Shutdown via adb

On Ubuntu Host PC

> 1)  $ adb -s <serialno> shell svc power shutdown

> 2)  Switch the RESET switch (SW2) and POWER switch (SW3) off after the display shows no signal


### Method 3: Shutdown via Android GUI

On Android GUI

1. Swipe down in the home screen.
   When the screen shown below is displayed, tap the power icon at the bottom center of the screen, then tap Power off.

    ![](images/shutdown_board.png){width="90%"}

2. Once the "shutting down" message disappears, turn SW2 to OFF.
3. Turn SW3 to OFF.

    ![](images/v2h_evk_shutdown.png){width="50%"}
