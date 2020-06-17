## EFIUTIL

A very simple utility to find and mount EFI partitions.

### Installation

Clone the archive and copy efiutil to /usr/local/bin.  Dependencies will install on first run.

```
$ git clone git@github.com:fewtarius/efiutil.git
$ test -d /usr/local/bin || sudo mkdir /usr/local/bin
$ sudo cp efiutil/efiutil /usr/local/bin
$ sudo chmod 755 /usr/local/bin/efiutil
```



### Usage

```bash
# efiutil --help

EFI Utility
-----------
Performs simple operations on one or many EFI partitions.

Warning: This utility must be run as root or via sudo.

    -b, --backup                     Backup EFI(s) to ~/EFIBackup
    -d, --device=DEVICE              Specify the device for operations
    -e, --external                   Perform operations on external disks
    -i, --internal                   Perform operations on internal disks
    -m, --mount                      Mount all matching EFI partitions
    -n, --info                       Show information for found devices
    -o, --bootloader=BOOTLOADER      Search for a specific bootloader or "all"
    -p, --path=PATH                  Specify the path for EFI backups
    -s, --silent                     Perform operations quietly.
    -u, --umount                     Unmount all matching EFI partitions
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
# efiutil --backup --internal
Mounted SPCC M.2 PCIe SSD Media : disk0s1 on /Volumes/disk0s1
Backing up EFI to EFI-SPCC_M.2_PCIe_SSD_Media-disk0s1-06162020-182849.zip
Unmounted SPCC M.2 PCIe SSD Media : disk0s1 from /Volumes/disk0s1
# ./efiutil --backup --bootloader OC
Found OC @ SPCC M.2 PCIe SSD Media : disk0s1
Found OC @ SanDisk Cruzer Glide 3.0 Media : disk2s1
No match for OC @ Flash Drive SM_USB20 Media : disk3s1
Available Bootloaders:
   BOOT
Mounted SPCC M.2 PCIe SSD Media : disk0s1 on /Volumes/disk0s1
Backing up EFI to EFI-SPCC_M.2_PCIe_SSD_Media-disk0s1-06162020-182949.zip
Unmounted SPCC M.2 PCIe SSD Media : disk0s1 from /Volumes/disk0s1
Mounted SanDisk Cruzer Glide 3.0 Media : disk2s1 on /Volumes/disk2s1
Backing up EFI to EFI-SanDisk_Cruzer_Glide_3.0_Media-disk2s1-06162020-182956.zip
Unmounted SanDisk Cruzer Glide 3.0 Media : disk2s1 from /Volumes/disk2s1
# ./efiutil --backup --bootloader OC --internal
Found OC @ SPCC M.2 PCIe SSD Media : disk0s1
Mounted SPCC M.2 PCIe SSD Media : disk0s1 on /Volumes/disk0s1
Backing up EFI to EFI-SPCC_M.2_PCIe_SSD_Media-disk0s1-06162020-183009.zip
Unmounted SPCC M.2 PCIe SSD Media : disk0s1 from /Volumes/disk0s1
```

