# AI Applications

Sample applications using AI for RZ/V2H Software Package for AOSP 15 can be obtained from the link below.

[https://github.com/renesas-rz/rzv_aosp_ai_apps](https://github.com/renesas-rz/rzv_aosp_ai_apps)

The lineup of AI applications is as follows:

| Application | Model | Input | Output | License |
|:---|:---|:---|:---|:---|
| Image Classification | ResNet18/ResNet50 | Image | HDMI | Apache License 2.0 |
| Object Detection | YOLOv8 | USB Camera | HDMI | AGPL-3.0*|
| Object Detection | YOLOv8 | USB Camera | H.264 stream (received on a Windows PC) | AGPL-3.0* |

>**Note**:
>The YOLOv8 applications in this section are available under a <a href="https://www.gnu.org/licenses/licenses.html" target="_blank" rel="noopener noreferrer">GNU General public license</a>.
For the details of the license for each sample application and each model, please refer to the license file included in each directory of the sample applications.

If you are porting a Linux AI application to Android, please refer to the [AI Application Porting Guide](../ai-application-porting-guide/index.md).
