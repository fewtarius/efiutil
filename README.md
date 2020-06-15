## EFIUTIL

A very simple utility to find and mount EFI partitions.

### Installation

Clone the archive and copy efiutil to /usr/local/bin.  Dependencies will install on first run.

### Usage

```bash
# efiutil --help

EFI Utility
-----------
Performs simple operations on one or many EFI partitions.

Warning: This utility must be run as root or via sudo.

    -b, --bootloader=BOOTLOADER      Search devices for a specific bootloader or "all", CASE SENSITIVE.
    -d, --device=DEVICE              Specify the device for operations.
    -e, --external                   Perform operations on external disks.
    -i, --internal                   Perform operations on internal disks.
    -m, --mount                      Mount all matching EFI partitions.
    -n, --info                       Show information for found devices
    -u, --umount                     Unmount all matching EFI partitions.
```



### Examples

```bash
# efiutil --mount --internal
Mounted SPCC M.2 PCIe SSD Media : disk0s1 on /Volumes/disk0s1
# efiutil --info --external
disk2s1:
    Type: EFI
    MountPoint:
    Manufacturer: SanDisk Cruzer Glide 3.0 Media
    Ejectable: true
    Internal: false
    RootDevice: disk2

disk3s1:
    Type: DOS_FAT_32
    MountPoint:
    Manufacturer: Flash Drive SM_USB20 Media
    Ejectable: true
    Internal: false
    RootDevice: disk3
# ./efiutil --info --internal
disk0s1:
    Type: EFI
    MountPoint:
    Manufacturer: SPCC M.2 PCIe SSD Media
    Ejectable: false
    Internal: true
    RootDevice: disk0
    
# efiutil --umount --internal --bootloader OC
Found OC @ SPCC M.2 PCIe SSD Media : disk0s1
Unmounted SPCC M.2 PCIe SSD Media : disk0s1 from /Volumes/disk0s1
# ./efiutil --mount --internal
Mounted SPCC M.2 PCIe SSD Media : disk0s1 on /Volumes/disk0s1
slartibartfast:efiutil # ./efiutil --info --internal
disk0s1:
    Type: EFI
    MountPoint: /Volumes/disk0s1
    Manufacturer: SPCC M.2 PCIe SSD Media
    Ejectable: false
    Internal: true
    RootDevice: disk0

#
```

