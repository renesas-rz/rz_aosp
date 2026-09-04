## **Configure display resolution**

### Booting without video parameter set

By default, HWComposer selects highest resolution (up to HD 1280x720 60fps).

### Booting with video parameter set

1)  Power on the device and interrupt autoboot.

2)  Execute: **editenv bootargs**

3)  Append to bootargs:
    ```text
    androidboot.display.res.HDMI=<width>x<height>@<refresh-rate>
    ```
Example:

bootargs: **androidboot.display.res.HDMI=720x480@60**

4)  Execute: **saveenv**
