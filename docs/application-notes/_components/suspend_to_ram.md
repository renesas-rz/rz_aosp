## **Suspend-to-RAM**

Suspend-to-RAM (S2R) mode helps achieve low power consumption, enables faster system startup than a cold boot, and preserves the system state during suspension.

| Feature | Status |
| :--- | :--- |
| Graphics | Partially Supported. May fail to suspend at some cases |
| Codecs | Supported |

!!! note
    "Supported" status means the feature has passed sanity checks only and does not guarantee the operation of full functionality. Others are not tested and may not work.

**Use the following commands on the Android console to enter Suspend-to-RAM mode.**

```bash
su
echo 0 > /sys/module/printk/parameters/console_suspend
echo deep > /sys/power/mem_sleep
echo enabled > /sys/class/tty/ttySC3/power/wakeup
echo mem > /sys/power/state
```
{: .dollar }

Press the **SLEEP** button on the board to wake up the system from Suspend-to-RAM mode.
