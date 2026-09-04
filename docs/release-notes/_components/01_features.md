### **Feature List**

Feature List:

<div class="table-no-sort" markdown="1">

| **Feature** | **SMARC RZ/G3L** |
| :--- | :---: |
| Boot time (Actual measurement time) | Normal boot: 68 seconds<br>Optimize boot: 59 seconds<br> |
| GPIO Key (Power, Vol up/down) | Supported |
| Display Max | Max 1 screen (HDMI) |
| Display/Touch | Supported (via USB) |
| Audio | Audio output: via Headphone <br>Audio recording: Supported |
| Micro SD-Card | Supported |
| 3D Graphics | Supported - Mesa (panfrost) 26.1.1: OpenGL ES 3.1 |
| Bluetooth (OPP, HID, A2DP) | `Not Supported yet` |
| Bluetooth (PBAP, HFP) | `Not Supported` |
| Ethernet | Supported |
| Wi-Fi | Supported (1) |
| GPS/GNSS | `Not Supported` |
| Video Decode/Encode | Supported (2) |
| USB 2.0 Host/Func | Supported |
| USB 3.0 Host | `Not Supported` |
| USB Camera | Supported (3) |
| MIPI Camera | `Not Supported yet` |
| Suspend to RAM | Partial Supported |
| File Based Encryption (FBE) | `Not Supported yet` |
| Verified Boot | Supported |
| Multiple Display | `Not Supported` |
| Energy Aware Scheduler | `Not Supported (4)` |
| OTA | `Not Supported yet` |
| Watchdog | `Not Supported yet` |
| SDCard boot | Unofficial Supported (5) |
| Hardware keymint/gatekeeper | `Not Supported yet` |
| Fastboot UDP | `Not Supported` |
| eSD boot | Supported |
| Wi-Fi Direct (P2P) | `Not Supported yet` |
| Neural Networks | `Not Supported` |

</div>

“Supported” means “just pass sanity check”. It does not guarantee the operation of full functionality.

(1) It’s required to build image with "export ENABLE_WIFI_SUPPORT=true". <br>
Tested Device: [2AE / 2BC M.2 Module](https://www.embeddedartists.com/products/2ae-m-2-module/)

(2) Supported Decode/Encode H.264 (resolution from 80x80 to 1280x720).

(3) Tested USB devices: Logitech C270 and C930e (Maximum Support Resolution: 864x480).

(4) EAS does not support platforms with symmetric CPU topologies.

(5) Please refer [Using SDCard boot](../application-notes/index.md#using-sdcard-boot) for more details.


