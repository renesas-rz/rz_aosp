### **Feature List**

Feature List:

<div class="table-no-sort" markdown="1">

| **Feature** | **RZ/V2H EVK** |
| :--- | :---: |
| Boot time (Actual measurement time) | Normal boot: 106 seconds<br>Optimize boot: 95 seconds<br>(Android images on SD Card) |
| GPIO Key (Power, Vol up/down) | `Not Supported` |
| Display Max | Max 1 screen (HDMI) |
| Display/Touch | Supported (via USB) |
| Audio | Audio output: via Headphone (1)<br>Audio recording: Supported |
| Micro SD-Card | Supported |
| 3D Graphics | Supported (OpenGL ES + Vulkan) |
| ADSP | `Not Supported` |
| Bluetooth (OPP, HID) | Supported (2) |
| Bluetooth (PBAP, HFP, A2DP) | `Not Supported` |
| Ethernet | Supported |
| Wi-Fi | Supported (3) |
| Fake GPS | `Not Supported` |
| GPS/GNSS | `Not Supported` |
| Video Decode/Encode | Supported (4) |
| USB 2.0 Host/Func | Supported |
| USB 3.0 Host | Supported |
| USB Camera | Supported (5) |
| MIPI Camera | Supported (6) |
| Suspend to RAM | `Not Supported` |
| Telephony | `Not Supported` |
| File Based Encryption (FBE) | Supported |
| Verified Boot | Supported |
| Multiple Display | `Not Supported` |
| Energy Aware Scheduler | `Not Supported (7)` |
| OTA | Supported |
| Watchdog | `Not Supported` |
| SDCard boot | Supported (8) |
| Hardware keymaster/gatekeeper | `Not Supported` |
| Fastboot UDP | Supported (9) |
| eSD boot | Supported |
| Wi-Fi Direct (P2P) | `Not Supported` |
| Neural Networks | `Not Supported` |

</div>

“Supported” means “just pass sanity check”. It does not guarantee the operation of full functionality.

(1) Audio only supports sampling rate 44.1 kHz.

(2) It’s required to build image with "export ENABLE_BT_SUPPORT=true"

(3) It’s required to build image with "export USE_USB_WIFI=true"

(4) Supported Decode/Encode H.264 (resolution from 224x96 to 1920x1080) and H.265 (resolution from 256x96 to 1920x1080).

(5) Tested USB device: Logitech C930e.

(6) The CMOS sensor (OV5645) in the MIPI camera is no longer available and should not be used for mass production. Any software support provided is for evaluation purposes only.
To use MIPI Camera, please read [MIPI Camera module](../how-to-build-aosp-from-source-code/#mipi-camera-module)

(7) EAS does not support platforms with symmetric CPU topologies.

(8) No support external storage on SD1 slot when booting Android image by SD card on SD2 slot.

(9) It’s required to build image with "export USE_FASTBOOTD_FOR_UDP=true". Fastboot UDP does not work on Ethernet port (CN6).
