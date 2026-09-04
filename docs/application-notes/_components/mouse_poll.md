## **Mouse Polling Rate Configuration**

Graphics and video codec performance may be decreased when using a mouse with a polling rate higher than 125 Hz. This is due to increased CPU usage from processing more frequent input events.

### **Issue Description**

When using high-performance gaming mouse with polling rates which is higher than 125Hz, you may experience:

* Decreased graphics performance
* Video codec performance issues
* Audio playback problems
* Increased CPU usage

### **Workaround**

To workaround this issue, please limit the mouse polling rate to 125Hz by adding the `usbhid.mousepoll` kernel parameter to the boot arguments.

**Steps to configure:**

1. Power on board and interrupt at u-boot by pressing any key
2. **Edit boot arguments** to include the mouse polling parameter:

    ```bash
    editenv bootargs
    edit: <existing_bootargs> usbhid.mousepoll=8
    saveenv
    boot
    ```
    {: .diamond2}

### **Parameter Values**

Here are the current experiment of usbhid.mousepoll parameter:

| Value | Polling Rate | Description |
| :---: | :---: | :--- |
| 8 | 125 Hz | Recommended for general Android use |
| 4 | 250 Hz | Higher performance, may impact system |
| 2 | 500 Hz | High performance, likely to cause issues |
| 1 | 1000 Hz | Maximum rate, not recommended |

!!! note
    * These parameter values are based on **experimental testing**. Users can adjust the polling rate according to their specific requirements and system performance needs.
    * This configuration is particularly important when using high-end gaming mouse with Android systems.