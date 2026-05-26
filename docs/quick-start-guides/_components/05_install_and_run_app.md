## Application Installation and Run

This section explains how to run the Application.

### Install APK

This section explains how to install APK file to Android UI.

<span style="color:blue">**Requirements:**</span>

- To install the APK, you need to flash the prebuilt images and booting Android Environment successfully, referring to the [Flashing bootloader](#flashing-bootloader) and [Flashing images using fastboot](#flashing-images-using-fastboot).
- Connect the CN2 (RZ/V2H EVK) and Ubuntu Host PC using a MicroUSB cable.
- Connect the HDMI touch panel with USB. If you do not have one, you can substitute it with a HDMI display and a USB mouse connected to RZ/V2H EVK.

#### Step 1: Check the setting to install APK

1. Boot the RZ/V2H EVK according to the [Booting RZ/V2H EVK](#booting-rzv2h-evk).
   Open a terminal for adb (Android Debug Bridge) on your Ubuntu Host PC.
   
2. On Ubuntu Host PC, check the connection between RZ/V2H EVK and Ubuntu Host PC. The ID 18d1 should be displayed. 
    If the ID 18d1 is not displayed, check the physical connection:
    ```sh
    $ lsusb
    ```

    If the following output is displayed, you have successfully connected to the RZ/V2H EVK.
    > Bus 003 Device 008: ID 18d1:4e11 Google Inc. Nexus One

3. Check whether an Android-specific udev rules file such as 51-android.rules or 99-android.rules exists in /etc/udev/rules.d/. 
    ```sh
    $ ls /etc/udev/rules.d/
    ```

4. If the rules file does not exist, create a rules file that grants device access permissions to the plugdev group.<br>
   In this example, create 51-android.rules using a text editor and enter the following content, then save the file:
    ```sh
    SUBSYSTEM=="usb", ATTR{idVendor}=="18d1", MODE="0666", GROUP="plugdev"
    ```
    SUBSYSTEM=="usb": Targets only USB devices
    <br>ATTR{idVendor}==“18d1": Set the vendor ID (Geogle: 18d1) of the device
    <br>MODE="0666": Allows access for all user
    <br>GROUP="plugdev": Grants access if the user belongs to the plugdev group

5. If the rules file such as 51-android.rules or 99-android.rules already exists but does not contain the same entries, append the same entries to the file.

6. Reload the rules to apply the changes
    ```sh
    $ sudo udevadm control --reload-rules
    $ sudo udevadm trigger
    ```

7. Add the current user to the plugdev group.
    ```sh
    $ sudo usermod -aG plugdev $USER
    ```

8. Log out and log back in, then restart the RZ/V2H EVK. ([Shutdown RZ/V2H EVK](#shutdown-device)</a>/[Booting RZ/V2H EVK](#booting-rzv2h-evk))
   
#### Step 2: Install APK file using adb 

1. Move to the prebuilt binary directory. 
    ```sh
    $ cd <your working dir>/RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images
    $ chmod a+x *
    ```
2. Verify that the connection to the RZ/V2H EVK and Ubuntu Host PC is established using the following command:
    ```sh
    $ ./adb devices -l
    ```

    If the following output is displayed, you have successfully connected to the RZ/V2H EVK.
    > List of devices attached<br>
    > XXXXXXXX   device usb:xxx product:rzv2h_evk_ver1 model:RZV2H_EVK_VER1_r9a09g057h4_evk device:rzv2h_evk_ver1 transport_id:x

3. If you already have installed the ResNet application, uninstall the application.

    ```sh
    $ ./adb uninstall com.tutorial
    ```

4. Install the built application on V2H EVK board using the following command. The message "Performing Streamed Install" will be displayed. Wait until "Success" message is displayed.

    If you are using the APK file provided by Renesas, execute the following command.
    ```sh
    $ wget https://github.com/renesas-rz/rzv_aosp_ai_apps/releases/download/v1.00/resnet_app-release.apk
    $ ./adb install resnet_app-release.apk
    ```

<span style="color:red">**Note:**</span> If the APK file installation fails, please use the `adb` tool from `platform-tools` following the below steps and perform the installation again.

- Download and extract the `platform-tools` package from Google

    ```bash
    $ cd <your working dir>
    $ wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
    $ unzip platform-tools-latest-linux.zip
    $ export PATH=<path to your working dir>/platform-tools:$PATH
    ```

- Confirm the new adb tool before using

    ```bash
    $ which adb
    ```
    The output should be:
    ```text
    <path to your working dir>/platform-tools/adb
    ```

- Please update your adb command when switching to use `adb` from `platform-tools`

    Old command (use `adb` tool from `prebuilt-images`)
    ```bash
    $ ./adb install <path to your working dir>/RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images/resnet_app-release.apk
    ```

    New command (use `adb` tool from `platform-tools`)
    ```bash
    $ adb install <path to your working dir>/RTK0EF0188Z76001ZJ_v15.3.0_prebuilt-images/prebuilt-images/resnet_app-release.apk
    ```

<span style="color:red">**Note:**</span> These commands are executed on Ubuntu Host PC

### Run the Application

This section explains how to run the Application.

<span style="color:blue">**Requirements:**</span>

- To run the application, you have completed the installation of the APK file by following the instructions in [Install APK file using adb](#install-apk).
- Connect the HDMI touch panel with USB. If you do not have one, you can substitute it with a HDMI display and a USB mouse connected to RZ/V2H EVK.

#### Step 1: Boot Android Environment
1. Confirm if Android environment is booted successfully, the following screen is displayed:<br>
   After [Booting RZ/V2H EVK](#booting-rzv2h-evk), the following screen will appear after a few minutes.

    ![](images/boot_complete.png){width="100%"}

2. Swipe up to open the home screen, When the home screen appears, tap the square icon at the bottom-right corner of the screen, and then tap the icon at the bottom-center of the next screen.

    ![](images/application_list.png){width="90%"}

#### Step 2: Run the Application
1. Click to TutorialApp icon to start the application

    ![](images/tutorialapp_icon.png){width="90%"}

2. The application screen will appear. Click Run to start AI inference
  
    ![](images/run_AI_Inference.png){width="90%"}

3. To change the AI model, tap the triangle icon at the top-right of the screen, select a model from the drop-down menu, and then tap RUN. 

    ![](images/cng_AI_model.png){width="90%"}

4. To change the DRP-AI frequency, enter the frequency index n (1 <= n <= 127) in the Optional field, and then tap the RUN.
   The relationship between the DRP-AI frequency and the frequency index n is as follows:
   Without an index, or with index 1 or 2: 1 GHz. For index n (3 <= n <= 127): 1260/(n-1) MHz.

    ![](images/cng_drpai_freq.png){width="90%"}

5. Example of the Inference result is displayed the same as:
    ```
    Selected model: resnet18_torch

    [TIME] Pre Processing Time: 3.83 msec.
    [TIME] AI Processing Time: 17.69 msec.
    Output data type : FP16.
    Result -----------------------
    Top 1 [ 66.0%] : [beagle]
    Top 2 [ 13.0%] : [English foxhound]
    Top 3 [ 11.4%] : [Walker hound, Walker foxhound]
    Top 4 [  5.9%] : [basset, basset hound
    Top 5 [  0.7%] : [bloodhound, sleuthhound]
    ```

#### Step 3: Close the Application and shutdown the RZ/V2H EVK
1. To exit the application, tap the square icon at the bottom-right of the screen. 
   When the screen shown below is displayed, swipe the application to the right. 
   The CLEAR ALL button will appear on the left side of the screen. Tap this button. 
   The application will close and return to the home screen.

    ![](images/close_application.png){width="90%"}

    > If you are using a touch panel, you can also close the application by flicking it up.

2. To shutdown the RZ/V2H EVK, swipe down in the home screen.
   When the screen shown below is displayed, tap the power icon at the bottom center of the screen, then tap Power off.
   Once the "shutting down" message disappears, turn off SW2 and then SW3 to power off the RZ/V2H EVK.

    ![](images/shutdown_board.png){width="90%"}

### Application: Configuration 
#### AI Processing time
|AI model | AI Processing time|
|:---|:---|
|resnet50_v1_onnx | Approximately 7 ms  |
|resnet18_torch | Approximately 6 ms  |
|resnet50_tflite| Approximately 50 ms  |
|resnet50_v1_onnx_cpu| Approximately 693 ms  |

<span style="color:blue">**Note:**</span> The AI ​​Processing time mentioned above does not include the AI Processing time of first time.

#### Processing

|Processing | Details |
|:---|:---|
|Pre Processing Time | Processed by DRP-AI. <br> |
|AI Processing Time | Processed by DRP-AI and CPU. |

### License

Apache License 2.0<br>
For licensing information regarding AI models, please refer to the source from which each model was obtained.

---

This concludes the explanation of the ResNet Console Application for *RZ/V2H Software Package for AOSP 15*.
