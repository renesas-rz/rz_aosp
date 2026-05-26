### **Known issues/Limitation**

| No. | Issue |
| :---: | :--- |
| 1 | Chrome crashes because it requires 32-bit support. Currently, we do not support 32-bit on AOSP 15. So, it is marked as **software limitation**. WORKAROUND: Using Firefox.|
| 2 | Low performance was observed when playing back 60p streams with GPU scaling (e.g., Playing back HD stream on a Full HD display). Please check part [GPU limitation](../application-notes/index.md#gpu-limitation)|
| 3 | H.265 Decode: Temporary visual artifacts may **rarely** occur during fast forward/rewind operations. Normal playback resumes once the operation completes.|
| 4 | Horizontal noise/flickering when changing mode on MXPlayer when playback H264 224x96 (or some codecs random cases) due to **high GPU usage**. Please check part [GPU limitation](../application-notes/index.md#gpu-limitation)|
| 5 | Using Screen Record application accessed from Quick Setting to record screen can cause soft reboot on FBE (File-Based encryption) environment after hit stop button. Please check part [Screen record issue from Quick Setting](../application-notes/index.md#screen-record-issue-from-quick-settings)|
