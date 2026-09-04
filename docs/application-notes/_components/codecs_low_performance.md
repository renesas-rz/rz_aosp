## **Codecs low performance**

By default, when playing a video whose resolution is different from the display resolution (For example: Playback 800x600 video on display
resolution 1280x720), the GPU must be used for handling both:

- video scaling
- layer composition

This additional workload causes high GPU usage and leads to low video playback performance.

To improve video playback performance on RZ/G3L, Image Scaling Unit (ISU) scaling and GPU scaling have been integrated into the Codec 2.0 HAL (C2 HAL).
The C2 HAL pre-scales the video layer so that it matches with the display resolution prior to composition.

The ISU scaling and GPU scaling are used by default to scale the video buffer, and the scaled video layer is then handled directly by the display driver through the overlay plane. 
This reduces the GPU workload by avoiding unnecessary GPU scaling and composition.

The ISU scaling supports video resolutions from 640 × 360 to 1280 × 720. GPU scaling is used for video resolutions lower than 640 × 360.

**Current limitations of current GPU Scaling implementation**

- Low performance may still occur when playing 60 FPS videos.
- Video playback may be frozen when the mouse is moved during playback.

**How to disable C2 HAL Pre-scaling:**

If it’s required to disable the default Pre-scaling feature, please execute the command below via adb shell:

* On host PC, execute command:

```bash
adb root # userdebug or eng build only
adb shell setprop persist.vendor.c2.prescale.enable 0
adb shell setprop persist.sys.media.prescale.enable 0
adb shell stop media && sleep 1 && adb shell start media
adb shell stop vendor-c2-hal-1-0 && sleep 1 && adb shell start vendor-c2-hal-1-0

```
{: .dollar }

!!! danger "CAUTION"
        It’s permanent change even users reboot the device

