## **Get RZ AOSP source code**

Clone android local package

```bash
$ cd <your working directory>
$ export ANDROID_BUILD_DIR=`pwd`
$ cd ${ANDROID_BUILD_DIR}
$ git clone https://github.com/renesas-rz/aosp_local_package.git -b android15-26q2
```

Checking the content of the source by listing items:

```bash
$ tree -L 1 ${ANDROID_BUILD_DIR}/aosp_local_package
```

The result should be:

```text
aosp_local_package/
├── additional_patches
├── buildenv.sh
├── modified-aosp-projects.xml
├── RELFILES
├── renesas-projects.xml
└── walkthrough.sh
```

Jumping to `aosp_local_package` directory
```bash
$ cd ${ANDROID_BUILD_DIR}/aosp_local_package
$ export workspace=$(pwd)
$ chmod a+x -R *
```

Note: Please make sure that all scripts have “execute” permission

```bash
$ export TARGET_SOC=r9a09g057
$ ./walkthrough.sh RZV2H_EVK_VER1
```

Please confirm this message

<span style="color:green">Done : TARGET= RZV2H_EVK_VER1</span>
