# Lab 4 — Storage: Partition, Mirror, Fail, Recover

## Windows

- System disk (Disk 0): 64 GB, GPT.
- Firmware: UEFI.
- New disk (Disk 1): 2 GB, GPT.
- Partition: E:
- Filesystem: NTFS.
- Volume label: LAB4.

GPT was selected because it supports disks larger than 2 TB, more than four partitions, and UEFI boot.


### Get-Disk output

Number Friendly Name                    Serial Number                                      HealthStatus OperationalStatus Total Size Partition Style
0      VMware Virtual NVMe Disk         9244_D8DB_D831_4C8B_000C_296A...                   Healthy      Online             64 GB      GPT
1      VMware Virtual NVMe Disk         E557_00AC_FE9F_99B2_000C_296B...                   Healthy      Online              2 GB      GPT

### Get-Partition -DiskNumber 1 output

PartitionNumber  DriveLetter  Offset     Size      Type
1                             17408      15.98 MB  Reserved
2                E            16777216   1.98 GB   Basic

### Get-Volume -DriveLetter E

DriveLetter  FriendlyName  FileSystemType  DriveType  HealthStatus  OperationalStatus  SizeRemaining  Size
E            LAB4          NTFS            Fixed      Healthy       OK                 1.97 GB         1.98 GB

### Firmware

UEFI

## Linux layout — before

NAME                       SIZE TYPE  FSTYPE            MOUNTPOINT
loop0                     66.8M loop  squashfs          /snap/core24/2124
loop1                     66.8M loop  squashfs          /snap/core24/1643
loop2                      1.5M loop  squashfs          /snap/hwctl/131
loop3                      1.5M loop  squashfs          /snap/hwctl/123
loop4                     44.7M loop  squashfs          /snap/snapd/28254
loop5                     50.1M loop  squashfs          /snap/snapd/27710
sda                         40G disk                    
├─sda1                       1M part                    
├─sda2                       2G part  ext4              /boot
└─sda3                      38G part  LVM2_member       
  └─ubuntu--vg-ubuntu--lv   19G lvm   ext4              /
sdb                          2G disk                    
└─sdb1                       2G part  linux_raid_member 
  └─md0                      2G raid1                   
sdc                          2G disk                    
└─sdc1                       2G part  linux_raid_member 
  └─md0                      2G raid1                   
sdd                          2G disk                    
sr0                       1024M rom                     
sr1                        2.7G rom   iso9660           


## RAID 1 states

### Healthy

See `evidence/array-healthy.txt`.

### Degraded

See `evidence/array-degraded.txt`.

### Data integrity after failure

The checksums before and after the disk failure matched (`MATCH`), confirming that the data remained intact.

See:
- `evidence/checksum-before.txt`
- `evidence/checksum-after-failure.txt`

### Rebuilt

The RAID 1 array was restored using `/dev/sdb1` and `/dev/sdd1`.

Final status: `[2/2] [UU]`.

See `evidence/array-rebuilt.txt`.

## Linux layout — after the rebuild

NAME                       SIZE TYPE  FSTYPE            MOUNTPOINT
loop0                     66.8M loop  squashfs          /snap/core24/1643
loop1                     66.8M loop  squashfs          /snap/core24/2124
loop2                      1.5M loop  squashfs          /snap/hwctl/131
loop4                      1.5M loop  squashfs          /snap/hwctl/123
loop5                     44.7M loop  squashfs          /snap/snapd/28254
loop6                     32.5M loop  squashfs          /snap/snapd/28332
sda                         40G disk                    
├─sda1                       1M part                    
├─sda2                       2G part  ext4              /boot
└─sda3                      38G part  LVM2_member       
  └─ubuntu--vg-ubuntu--lv   19G lvm   ext4              /
sdb                          2G disk                    
└─sdb1                       2G part  linux_raid_member 
  └─md0                      2G raid1 ext4              
sdc                          2G disk                    
sdd                          2G disk                    
└─sdd1                       2G part  linux_raid_member 
  └─md0                      2G raid1 ext4              
sr0                       1024M rom                     
sr1                        2.7G rom   iso9660           

| Role | Device |
|---|---|
| Mirror half A | `/dev/sdb1` |
| Failed half | `/dev/sdc1` |
| Replacement | `/dev/sdd1` |

## The question

Your colleague deleted the wrong file from the mirror an hour ago. Does RAID 1 help?

No. RAID 1 mirrors data across disks, so accidental deletion is also replicated to the other disk. RAID 1 protects against disk failure, not accidental deletion. Regular backups with historical versions are needed to recover deleted files.