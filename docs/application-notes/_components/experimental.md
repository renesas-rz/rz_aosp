## **Experimental features**

### Flexible Graphics

By default, Mali graphics is used. If users want to use Angle/Mesa (panfrost) graphics, please follow the steps below:

1) Power on the device and interrupt autoboot.

2) Execute the commands below on target board

```text
Switch between Mali/Angle/Mesa (panfrost) Graphics
=> editenv egl
        mali: Booting with Mali Graphics (default)
        mesa: Booting with Mesa (panfrost) Graphics
        angle: Booting with Angle Graphics
=> saveenv
=> boot
```

This implementation is intended to offer a flexible method for saving time on debugging Graphics issues.

<span style="color:red">**Note:**</span> Angle/Mesa graphics are experimental features. Some functionalities are <span style="color:red">NOT</span> supported yet. It’s only used for feasibility checking.

### Enable optional features

Wi-Fi (via TP-LINK Archer T4U AC1200 Wireless Dual Band USB 3.0 Adapter – version 1) and Bluetooth (via USB Bluetooth 5.0 Orico BTA-608) features are supported optionally via USB dongle. So, it’s not enabled by default. If users want to use these features, please "<span><strong>export ENABLE_BT_SUPPORT=true</strong></span>" and "<span><strong>export USE_USB_WIFI=true</strong></span>" then rebuild Android images.
