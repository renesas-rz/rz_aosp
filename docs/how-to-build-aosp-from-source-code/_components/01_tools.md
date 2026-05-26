!!! warning "Notice"
	The command in this section will be executed on the **Ubuntu Host PC**.

## **Tools & Dependency packages**

Prerequisite packages for building the Android Filesystem (**Note:** This is with reference to Ubuntu 20.04 64-bit). Ubuntu 64-bit is required for the cross-compilation of Android Filesystem.

Setup build environment according to Google Android setup guide (follow **Installing required packages**): <https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment>

```bash
$ sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev
$ sudo apt-get install libc6-dev-i386 x11proto-core-dev libx11-dev lib32z1-dev
$ sudo apt-get install libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
```

<div style="border: 2px solid red; padding: 15px; background-color: #ffffe0; margin-bottom: 30px">
    In addition, it's required to <span style="color:red">install "python-is-python3", "python-crypto", "liblz4-tool", "libssl-dev" and "lzop"</span> package. "python-is-python3" is used for "repo", "python-crypto" is used into the python scripts. "liblz4-tool" package is used into the compress tool which builds a kernel, "libssl-dev" is used for compiling kernel 4.19 and newer, "lzop" is used as a compressor similar to gzip. Below version packages were used to confirm this BSP version.
</div>

| Package | Version |
| :--- | :---: |
| python-is-python3 | - |
| python-crypto | 2.6.1-13ubuntu2 |
| liblz4-tool | 1.9.2-2ubuntu0.20.04.1 |
| libssl-dev | 1.1.1f-1ubuntu2.24 |
| lzop | 1.04-1 |


```bash
$ sudo apt-get install python-is-python3 python-crypto liblz4-tool libssl-dev lzop
```

To build Mesa Graphics, the following tools and development dependencies must be installed on the build host. For more details, please visit: <https://docs.mesa3d.org/install.html#compiling-and-installing>

```bash
$ sudo apt-get install python3-pip
$ sudo pip3 install --upgrade meson ninja mako PyYAML
```

<span style="color:red">**Note:**</span> **meson** package version should be “**1.1.0**” or higher for building Mesa 24.3.3

Please install the following packages when users need to set up build environment by using Ubuntu 20 Docker container. This is just for reference only and note that Renesas official test is on natively-installed Ubuntu 20

```bash
$ sudo apt-get install rsync libncurses5
```

<span style="color:red">**Note:**</span> Recommended **python3** version: **3.8.10** for Ubuntu 20.04

Please install the following package when users need to set up build environment by using Ubuntu 22.04 Docker container. This is just for reference only and note that Renesas official test is on natively-installed Ubuntu 22.04

```bash
$ sudo apt-get install pkg-config
```
