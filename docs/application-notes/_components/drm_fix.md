## **Disabling non-blocking feature in drm_hwcomposer**

Open Camera, MX Player and other application does not work properly on RZ/V2H due to timing issue between GPU rendering thread and drm hwcomposer.

By default, disabling non-blocking feature is a workaround to resolve above problems.

User can re-enable it by executing below command:

```bash
# On host PC, execute command:
$ adb root
$ adb shell setprop vendor.hwc.drm.disable_non_block 0
```

