## **Get RZ AOSP source code**

Clone android local package

```bash
cd <your working directory>
export ANDROID_BUILD_DIR=`pwd`
cd ${ANDROID_BUILD_DIR}
git clone https://github.com/renesas-rz/aosp_local_package.git -b android17-26q3
```
{: .dollar }

Checking the content of the source by listing items:

```bash
tree -L 1 ${ANDROID_BUILD_DIR}/aosp_local_package
```
{: .dollar }

The result should be:

```text
aosp_local_package/
├── buildenv.sh
├── modified-aosp-projects.xml
├── RELFILES
├── renesas-projects.xml
└── walkthrough.sh
```

Jumping to `aosp_local_package` directory
```bash
cd ${ANDROID_BUILD_DIR}/aosp_local_package
export workspace=$(pwd)
chmod a+x -R *
```
{: .dollar }

!!! note
     Please make sure that all scripts have “execute” permission

!!! note "Optional"
    To achieve fetch reliability and build stability, user can refer AOSP mirror from [Q5. Using AOSP mirror for offline fetch](../frequently-asked-questions/index.md#q5-using-aosp-mirror-for-offline-fetch)

```bash
export TARGET_SOC=r9a08g046
./walkthrough.sh SMARC_RZG3L
```
{: .dollar }

Please confirm this message

<span style="color:green">Done : TARGET= SMARC_RZG3L</span>
