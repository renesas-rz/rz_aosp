## Sample Applications for RZ AOSP BSP

Use these three sample applications to verify and test the functionalities of the RZ AOSP BSP. You can find the source code as Git bundles in our [aosp_local_package repository](https://github.com/renesas-rz/aosp_local_package/tree/android17-26q3/RELFILES/sample_apps).

### Prerequisites: Clone the Repository
To access the bundle files, first clone the `aosp_local_package` repository:

```bash
export workdir=`pwd`
git clone https://github.com/renesas-rz/aosp_local_package.git -b android17-26q3
cd aosp_local_package/RELFILES/sample_apps/
```
{: .dollar }

### Summary Table

| Application | Source | Build Method | Purpose |
| :--- | :--- | :--- | :--- |
| **ApiDemos** | AOSP (with Renesas RZ bug-fixes) | AOSP Build System | Android APIs tests: Graphics/Camera/General Android APIs |
| **Grafika** | [Grafika (Google)](https://github.com/google/grafika) | Android Studio | Codecs/Graphics samples |
| **Video Playback sample** | Renesas RZ | Android Studio | Video playback sample application with Renesas H264 Hardware Decoder (using Media3 APIs) |

---

### How to Use

To use these applications, you need to unbundle the provided files into a local Git repository. Please follow the specific commands for each application below.

#### 1. ApiDemos
*   **Commands:**

```bash
cd $workdir/aosp_local_package/RELFILES/sample_apps/
mkdir ApiDemos
cd ApiDemos/
git init
git fetch $workdir/aosp_local_package/RELFILES/sample_apps/apidemos.bundle origin/android-17.0.0_r1:origin/android-17.0.0_r1
git checkout origin/android-17.0.0_r1
```
{: .dollar }

#### 2. Grafika
*   **Commands:**

```bash
cd $workdir/aosp_local_package/RELFILES/sample_apps/
mkdir Grafika
cd Grafika/
git init
git fetch $workdir/aosp_local_package/RELFILES/sample_apps/grafika.bundle origin/android14-dev:origin/android14-dev
git checkout origin/android14-dev
```
{: .dollar }

#### 3. Video Playback Sample
*   **Commands:**

```bash
cd $workdir/aosp_local_package/RELFILES/sample_apps/
mkdir video_playback_sample
cd video_playback_sample/
git init
git fetch $workdir/aosp_local_package/RELFILES/sample_apps/video_playback_sample.bundle origin/main:origin/main
git checkout origin/main
```
{: .dollar }
