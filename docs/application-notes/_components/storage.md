## **USB Storage / micro SD-Card Usage**

To use USB Storage / micro SD-Card on Android GUI, user should format and create partition for USB Storage / micro SD-Card on **Ubuntu Host PC** beforehand:

<span style="color:red">**Note:**</span> before formatting, please confirm carefully **/dev/sdX** of your Storage devices (by 'lsblk' command)

```bash
# Format USB Storage / micro SD-Card

# Plug in USB Storage / micro SD-Card on Ubuntu Host PC, and delete all existed partitions:
$ sudo fdisk /dev/sdX (X = storage devices)
# type ‘d’ and type ‘Enter’                            # Loop until there is no existed partition)
# type ‘w'                                             # Alter changing

# Create new partition (1 partition is OK)
$ sudo fdisk /dev/sdX (X = storage devices)
# type ‘n’ and type ‘Enter’ (4 times)                  # Create new partition
# type ‘w’                                             # Alter changing

# Change partition type
$ sudo fdisk /dev/sdX (X = storage devices)
# type ‘t’ and type ‘c’                                # Format as W95 FAT32 (LBA)
# type ‘w'                                             # Alter changing

# Format partition as FAT32
$ sudo mkfs.vfat /dev/sdX1                             # (X = storage devices; 1 = partition number)

# Plug USB Storage/micro SD-Card on board and use it!
```
