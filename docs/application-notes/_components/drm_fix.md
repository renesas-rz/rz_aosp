## **Disabling non-blocking feature in drm_hwcomposer**

Open Camera, MX Player, Antutu and other application does not work properly on SMARC RZ/G3L due to timing issue between GPU rendering thread and drm hwcomposer.

By default, disabling non-blocking feature is a workaround to resolve above problems.

User can re-enable it by executing below command:

* On host PC, execute command:

```bash
adb root
adb shell setprop vendor.hwc.drm.disable_non_block 0
```
{: .dollar }

