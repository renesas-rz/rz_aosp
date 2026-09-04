## **Enable and Run Sample Applications**

This section explains how to enable and run the Sample Applications.

### Enable Sample Applications

#### Enable demo applications with environment variable

* Step 1: Set the demo support environment variable:

   ```bash
   export SUPPORT_DEMO=true
   ```
   {: .dollar }

* Step 2: Re-build the Android image following the instructions in [Building Android, IPL, U-Boot, and Kernel sources](../how-to-build-aosp-from-source-code/index.md#building-android-ipl-u-boot-and-kernel-sources)


### Run the Application

This section explains how to run the Application.

!!! note
    * Connect the HDMI touch panel with USB. If you do not have one, you can substitute it with a HDMI display and a USB mouse connected to SMARC RZ/G3L.

#### Step 1: Boot Android Environment
1. Confirm if Android environment is booted successfully, the following screen is displayed:<br>
   After [Booting SMARC RZ/G3L](#booting-smarc-rzg3l), the following screen will appear after a few minutes.

    ![](images/boot_complete.png){width="100%"}

2. Swipe up to open the home screen, When the home screen appears, swipe up to get UI of list of application.

    ![](images/application_list.png){width="90%"}

#### Step 2: Run the Application

##### Simple Playback Sample App

1. Prepare media (video) via "adb push"

2. Click to Simple Playback Sample App icon to start the application

    ![](images/simpleplayback_icon.png){width="90%"}

3. The application screen will appear. Swipe up to show all videos
  
    ![](images/run_simpleplayback.png){width="90%"}

4. Choose a video to play.

!!! note
    * Can not detect media files when use adb shell command to push video from host machine to device. (Workaround: Reboot the device).
    * After playback video at the end, the app stops at last frame instead of back to main screen.

##### Grafika

1. Click to Grafika App icon to start the application

    ![](images/grafika_icon.png){width="90%"}

2. The application screen will appear the list of grafika test cases

    ![](images/grafika_run.png){width="90%"}

3. Choose a testcase to test.

!!! note
    Demo/Grafika fails for Play video (TextureView) and Play video (SurfaceView):  gen-slider.mp4 --> Crash application (Grafika keep stopping)


#### Step 3: Close the Application

To exit the application, tap the square icon at the bottom-right of the screen. 
When the screen shown below is displayed, swipe the application to the right. 
The **CLEAR ALL** button will appear on the left side of the screen. Tap this button. 
The application will close and return to the home screen.

![](images/close_application.png){width="90%"}

!!! note
     If you are using a touch panel, you can also close the application by flicking it up.





