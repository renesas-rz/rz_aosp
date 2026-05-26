## **GPU Limitation**

Mali G-31 GPU is used on RZ/V2H. It has one single-pixel shader core only. GPU usage may become very high in some use cases. In addition, the display driver supports up to 2 hardware planes. Due to these hardware limitations, high GPU usage may occur and can lead to the following issues:

- Codecs low performance during some video playback scenarios (60fps video playback)
- Flickering/horizontal noise when multiple layers are displayed

Here is an example of “GPU usage (GPU active)” is high when opening multiple applications:
<p align="center">
  <img src="images/high_gpu_usage.jpg" alt="High GPU Usage" width="90%">
</p>
<p align="center"> Figure. High GPU usage - captured by Arm Streamline </p>

### Codecs low performance

The current hardware does not include a dedicated hardware scaler. Therefore, when playing a video whose resolution is different from the display resolution (For example: Playback 1280x720 video on display resolution 1920x1080), the GPU must be used for handling both:

- video scaling
- layer composition

This additional workload causes high GPU usage and leads to low video playback performance.

To improve performance, the GPU Scaling implementation has been integrated into the C2 HAL. This feature pre-scales the video layer so that it matches with the display resolution prior to composition.

<span style="color:red">**Note**:</span> It is enabled by default to improve video playback performance.

**Current limitations of current GPU Scaling implementation:**

- Low performance may still occur when playing 60 FPS videos.
- The current implementation supports upscaling only. Downscaling is not supported.

**How to disable C2 HAL GPU Scaling:**

If it’s required to disable the default GPU Scaling feature, please execute the command below via adb shell:
```bash
# On host PC, execute command:
$ adb root # userdebug or eng build only
$ adb shell setprop persist.vendor.c2.prescale.enable 0
$ adb shell setprop persist.sys.media.prescale.enable 0
$ adb shell stop media && sleep 1 && adb shell start media
$ adb shell stop vendor-c2-hal-1-0 && sleep 1 && adb shell start vendor-c2-hal-1-0
```
<span style="color:red">**CAUTION:**</span> It’s permanent change even users reboot the device

### Flickering/horizontal noise when displaying multiple layers

Flickering or horizontal noise lines may be observed on the screen when displaying multiple layers (Example: opening multiple applications).

The display drivers support a maximum of 2 hardware planes. When 3 or more layers are displayed, the system falls back to GPU composition. The GPU usage may be increased sharply during this transition, leading the following issues:

- screen flickering (disappear after some seconds)
- horizontal noise lines (disappear after some seconds)

Currently, there is no available solution.
