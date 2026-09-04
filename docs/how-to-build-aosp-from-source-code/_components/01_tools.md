!!! warning "Notice"
	The command in this section will be executed on the **Ubuntu Host PC**.

## **Tools & Dependency packages**

Prerequisite packages for building the Android Filesystem (**Note:** This is with reference to Ubuntu 22.04 64-bit). Ubuntu 64-bit is required for the cross-compilation of Android Filesystem.

Setup build environment according to Google Android setup guide (follow **Installing required packages**): <https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment>

```bash
sudo apt-get install git-core gnupg flex bison build-essential zip curl zlib1g-dev
sudo apt-get install libc6-dev-i386 x11proto-core-dev libx11-dev lib32z1-dev
sudo apt-get install libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig
```
{: .dollar }

<div style="border: 2px solid red; padding: 15px; background-color: #ffffe0; margin-bottom: 30px">
    In addition, it's required to <span style="color:red">install "python-is-python3", "python3-cryptography", "liblz4-tool", "libssl-dev" and "lzop"</span> package. "python-is-python3" is used for "repo". "liblz4-tool" package is used into the compress tool which builds a kernel, "libssl-dev" is used for compiling kernel 4.19 and newer, "lzop" is used as a compressor similar to gzip. Below version packages were used to confirm this BSP version.
</div>

| Package | Version |
| :--- | :---: |
| python-is-python3 | 3.9.2-2 |
| python3-cryptography | 3.4.8-1ubuntu2.4 |
| liblz4-tool | 1.9.3-2build2 |
| libssl-dev | 3.0.2-0ubuntu1.26 |
| lzop | 1.04-2build2 |


```bash
sudo apt-get install python-is-python3 python3-cryptography liblz4-tool libssl-dev lzop
```
{: .dollar }

To build IPL, U-boot by script, the following tools must be installed on the build host.

```bash
sudo apt-get install srecord
```
{: .dollar }

To build Mesa Graphics, the following tools and development dependencies must be installed on the build host. For more details, please visit: <https://docs.mesa3d.org/install.html#compiling-and-installing>

```bash
sudo apt-get install python3-pip
sudo pip3 install --upgrade meson ninja mako PyYAML
```
{: .dollar }

!!! note
     **meson** package version should be “**1.1.0**” or higher

Please install the following packages when users need to set up build environment by using Ubuntu 22.04 Docker container. This is just for reference only and note that Renesas official test is on natively-installed Ubuntu 22.04

```bash
sudo apt-get install rsync libncurses5 pkg-config
```
{: .dollar }

!!! note
     Recommended **python3** version: **3.10.12** for Ubuntu 22.04
