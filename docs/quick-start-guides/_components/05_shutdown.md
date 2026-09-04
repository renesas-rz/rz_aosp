## **Shutdown device**

Shutdown the device as shown:

### Method 1: Shutdown via board's console

On board's console:

> 1) 
```bash
reboot -p
```
{: .dollar }

> 2) Press and Hold the Power button (POWER) for 2 seconds to power off the SMARC RZ/G3L after the display shows no signal

### Method 2: Shutdown via adb

On Ubuntu Host PC

> 1) 
```bash
adb -s <serial#> shell svc power shutdown
```
{: .dollar }

> 2)  Press and Hold the Power button (POWER) for 2 seconds to power off the SMARC RZ/G3L after the display shows no signal


### Method 3: Shutdown via Android GUI

On Android GUI

1. From top center of the screen, swipe down.
   When the screen shown below is displayed, tap the power icon at the bottom center of the screen, then tap Power off.

    ![](images/shutdown_board.png){width="90%"}

2. Once the "shutting down" message disappears.
3. Press and Hold the Power button (POWER) for 2 seconds to power off the SMARC RZ/G3L.

    ![](images/smarc_g3l_shutdown.png){width="50%"}
