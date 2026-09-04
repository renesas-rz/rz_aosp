## **USB Storage / micro SD-Card Usage**

To use USB Storage / micro SD-Card on Android GUI, user should format and create partition for USB Storage / micro SD-Card on **Ubuntu Host PC** beforehand:

!!! note 
    before formatting, please confirm carefully **/dev/sdX** of your Storage devices (by 'lsblk' command)

* Format USB Storage / micro SD-Card

* Plug in USB Storage / micro SD-Card on Ubuntu Host PC, and delete all existed partitions:

```bash
sudo fdisk /dev/sdX (X = storage devices)
```
{: .dollar }

```bash
type ‘d’ and type ‘Enter’                            # Loop until there is no existed partition)
type ‘w'                                             # Alter changing
```
{: .hash}

*  Create new partition (1 partition is OK)

```bash
sudo fdisk /dev/sdX (X = storage devices)
```
{: .dollar }

```bash
type ‘n’ and type ‘Enter’ (4 times)                  # Create new partition
type ‘w’                                             # Alter changing
```
{: .hash}

* Change partition type

```bash
sudo fdisk /dev/sdX (X = storage devices)
```
{: .dollar }

```bash
type ‘t’ and type ‘c’                                # Format as W95 FAT32 (LBA)
type ‘w'                                             # Alter changing
```
{: .hash }

* Format partition as FAT32

```bash
sudo mkfs.vfat /dev/sdX1                             # (X = storage devices; 1 = partition number)
```
{: .dollar }

* Plug USB Storage/micro SD-Card on board and use it!

