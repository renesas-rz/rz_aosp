### **Known Issues/Limitations**

| No. | Issue |
| :---: | :--- |
| 1 | Chrome crashes because it requires 32-bit support. Currently, we do not support 32-bit on RZ AOSP, so it is marked as a **software limitation**. **WORKAROUND:** Use Firefox.|
| 2 | Audio playback has noise when seeking.|
| 3 | Audio recording loses sound in the first few frames and has intermittent sound issues **randomly**.|
| 4 | USB camera recording with audio enabled loses sound after a few seconds until the end.|
| 5 | Grafika/TextureView (and SurfaceView) activities are not working properly.|
| 6 | ApiDemos: Activity animations and Drag and Drop are not working properly.|
| 7 | The target playback performance cannot be achieved for video resolutions of 224x96 and lower (both 30p and 60p) when using Crop mode in the MX Player application.|
| 8 | The target playback performance cannot be achieved for video resolutions ranging from 640x360 to lower (60p).|
| 9 | Devices with #AC0 or #BC0 in the part number, as well as RZ/G3L EVKIT with Lot # 0000308367 –0000309059 that incorporate these devices, have limitations in the MIPI DSI feature. For details, please contact a Renesas Electronics sales representative.|
