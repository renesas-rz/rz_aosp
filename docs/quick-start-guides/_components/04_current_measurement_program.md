## **Current Measurement Program**

The Current Measurement Program for the RZ/G series supports current and voltage monitoring, graph plotting, and data logging. The program is not officially supported on the SMARC RZ/G3L, but it is expected to operate correctly because the platform uses the same current-sensing hardware as the supported platforms.

Please reference detail at: 
<https://www.renesas.com/en/document/apn/rz-series-current-measurement-program>

In this section, the Current Measurement Program is used to measure current and voltage, plot graphs, and save data while the system is operating in S2R (Suspend-to-RAM) mode. This demonstrates the power-saving benefits of S2R mode.

###**How to use Current Measurement Program**

**Step 1:** Power off the board and connect USB cables as shown below:

<p align="center">
  <img src="images/current_measurement.jpg" alt="SMARC RZG3L connection to Current measurement" width="100%">
</p>
<p align="center"> Figure. SMARC RZG3L connection to Current measurement </p>

!!! note 
    When SER3_UART is connected to a Windows PC, run TeraTerm on the PC, select the correct COM port and change its Baud rate to 115200 (“Setup > Serial port…”).

**Step 2:** Set up the Current Meansurement application on the Windows PC.

a. Log in to Renesas website and download the Current Meansurement package from the link below: 
<https://www.renesas.com/en/document/swe/rz-series-current-measurement-program>

b. Extract the ZIP file twice and confirm that the extracted files match those shown below: 

<p align="center">
  <img src="images/current_measurement_app2.jpg" alt="Current Measurement Program executable file" width="100%">
</p>
<p align="center"> Figure. Current Measurement Program executable files </p>

c. Double click on **CurrentMeasurementAppFor5ch.exe** to start the program. Since the SMARC RZ/G3L supports only four channels, make sure to uncheck the 0x9E I2C address.

<p align="center">
  <img src="images/current_measurement_app3.jpg" alt="Current Measurement Program uncheck 9e I2C address" width="100%">
</p>
<p align="center"> Figure. Current Measurement Program with 0x9E I2C address unchecked </p>

d. Click the "Start/Stop" Button to start or stop measurement.

<p align="center">
  <img src="images/current_measurement_app4.jpg" alt="Start or Stop program" width="100%">
</p>
<p align="center"> Figure. Start or Stop measurement </p>

**Step 3:** Press the POWER button to boot Android.

<p align="center">
  <img src="images/current_measurement_app5.jpg" alt="Program show current when powerup Android" width="100%">
</p>
<p align="center"> Figure. Current and voltage measurements during Android boot </p>

**Step 4:** Wait for Android to finish booting, then open API Demos -> Graphics -> OpenGL ES -> Kube to run a graphics workload.

<p align="center">
  <img src="images/current_measurement_app6.jpg" alt="Voltage and current when playing back API Demos" width="100%">
</p>
<p align="center"> Figure. Voltage and current measurements while running API Demos </p>

**Step 5:** Run the following commands on the board console to enter [Suspend-to-RAM mode](../application-notes/index.md#suspend-to-ram):

```bash
su
echo 0 > /sys/module/printk/parameters/console_suspend
echo deep > /sys/power/mem_sleep
echo enabled > /sys/class/tty/ttySC3/power/wakeup
echo mem > /sys/power/state
```
{: .dollar }

**Step 6:** Resume from S2R mode by pressing the SLEEP button.

**Step 7:** Shut down the Android device by following the instructions in [Shutdown device](#shutdown-device) section.

**Step 8:** Press the POWER button to turn off the board.

The measurement results are then displayed as shown in the figure below:

<p align="center">
  <img src="images/current_measurement_app7.jpg" alt="Voltage and current show when S2R" width="100%">
</p>
<p align="center"> Figure. Voltage and current consumption in S2R mode </p>

