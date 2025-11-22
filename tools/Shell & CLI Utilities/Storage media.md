# Storage media and devices


## Linux and storage devices:
+ Linux has amazing capabilities for handling storage devices, whether physical storage such as hard disks, network storage, or virtual storage devices such as RAID (Redundant Array of Independent Disks) and LVM (Logical Volume Manager).


## Most storage media commands:
+ `mount`: Mount a ﬁle system.
+ `umount`: Unmount a ﬁle system.
+ `fsck`: Check and repair a ﬁle system.
+ `fdisk`: Manipulate disk partition table.
+ `mkfs`: Create a ﬁle system.
+ `dd`: Convert and copy a ﬁle.
+ `genisoimage`: (mkisofs) Create an ISO 9660  image ﬁle.
+ `wodim`: (cdrecord) Write data to optical storage media.
+ `md5sum`: Calculate an MD5 checksum.


---
# Mounting and Unmounting Storage Devices


## Mounting Process:
+ The ﬁrst step in managing a storage device is attaching the device to the ﬁle system tree. This process, called mounting.
+ Allows the device to interact with the operating system.


## File system tree in Linux and Windows :
+ Unix-like operating systems (like Linux) **maintain a single ﬁle system  tree** with devices attached at various points. 
+ This contrasts with other operating systems such as Windows that **maintain separate ﬁle system trees** for each device (for example C:\, D:\, etc.).
+ See [wiki Filesystem](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)
+ ![[Pasted image 20230510151351.png]]


## Fstab file:
+ In the time of the ancients, users had to manually mount these drives to a file location using the `mount` command. 
+ The `fstab` file became an attractive option because of challenges like this. 
+ It is designed to configure a rule where specific file systems are detected, then automatically mounted in the user's desired order every time the system boots. 
+ Not only is it less work over time, but it also allows the user to avoid load order errors that could eat up valuable time and energy.
+ See [fstab on debian](https://wiki.debian.org/fstab)


## File system table:
+ A ﬁle named `/etc/fstab` (short for “ﬁle system table”) lists the devices that are to be mounted at boot time or we can say lists hard disk partitions.
>>`cat /etc/fstab`
```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# systemd generates mount units based on this file, see systemd.mount(5).
# Please run 'systemctl daemon-reload' after making changes here.
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sdb2 during installation
UUID=a376f388-40e4-49ea-ba20-cf0afb2f0baa /               ext4    errors=remount-ro 0       1
# /boot/efi was on /dev/sdb1 during installation
UUID=0712-BF15  /boot/efi       vfat    umask=0077      0       1
# swap was on /dev/sdb3 during installation
UUID=c4a23c46-bcfe-47b9-b365-53078d5e1bdd none            swap    sw              0       0
```
>> `blkid`
```
/dev/nvme0n1p5: 
	LABEL="RECOVERY"
	BLOCK_SIZE="512"
	UUID="8E7E9C147E9BF2E7"
	TYPE="ntfs"
	PARTLABEL="Basic data partition"
	PARTUUID="1090bc5c-b8d8-42c3-b287-dbcdd6b934d8"

/dev/nvme0n1p3: 
	LABEL="OS"
	BLOCK_SIZE="512"
	UUID="C602C9AE02C9A431"
	TYPE="ntfs"
	PARTLABEL="Basic data partition"
	PARTUUID="acebf3eb-299d-4919-ab68-2665d406a42c"

/dev/nvme0n1p1: 
	LABEL="SYSTEM"
	UUID="12C7-F675"
	BLOCK_SIZE="512"
	TYPE="vfat"
	PARTLABEL="EFI system partition"
	PARTUUID="7f2f632b-b72c-4f24-97c7-552ff8266d6f"

/dev/nvme0n1p6: 
	LABEL="MYASUS"
	UUID="5270-960A"
	BLOCK_SIZE="512"
	TYPE="vfat"
	PARTLABEL="Basic data partition"
	PARTUUID="f636cb34-148b-4559-9038-21f80b530791"

/dev/nvme0n1p4: 
	LABEL="New Volume"
	BLOCK_SIZE="512"
	UUID="3C68C88468C83E80"
	TYPE="ntfs"
	PARTLABEL="Basic data partition"
	PARTUUID="64fbba7f-c06e-4943-a327-37f2eea5a885"

/dev/nvme0n1p2: 
	PARTLABEL="Microsoft reserved partition"
	PARTUUID="acbbc0f2-dba1-4265-8ee1-c59fd4897acf"

/dev/sdb1: 
	LABEL="8S"
	UUID="0467-67D0"
	BLOCK_SIZE="512"
	TYPE="exfat"
	PARTUUID="70b20518-01"

/dev/sda2: 
	UUID="a376f388-40e4-49ea-ba20-cf0afb2f0baa"
	BLOCK_SIZE="4096"
	TYPE="ext4"
	PARTUUID="51a3e40c-ee6e-49c2-b31a-90165a34d930"

/dev/sda3: 
	UUID="c4a23c46-bcfe-47b9-b365-53078d5e1bdd"
	TYPE="swap"
	PARTUUID="90b14e19-78ad-4fd7-94d0-338234f8da82"

/dev/sda1: 
	UUID="0712-BF15"
	BLOCK_SIZE="512"
	TYPE="vfat"
	PARTUUID="3c17d096-ab05-4c29-9484-0e8f1546f97f"
```
+ UUID is Universally Unique Identiﬁer.


## Field definitions:
+ `/etc/fstab` contains the following fields separated by a space or tab (as a table header): 
	+ `<file system>`.
	+ `<dir or mount point>`.
	+ `<type>`.
	+ `<options>`.
	+ `<dump>`.
	+ `<pass>`.
+ **File systems**:
	+ Defines the storage device (i.e. /dev/sda1).
+ **Mount point**:
	+ tells the mount command where it should mount the file system to.
+ **Type**:
	+ defines the file system type of the device or partition to be mounted. 
	+ Many different file systems are supported. 
	+ Some examples are: `ext2, ext3, reiserfs, xfs, jfs, smbfs, iso9660, vfat, ntfs, swap, and auto.` 
	+ The 'auto' type lets the mount command to attempt to guess what type of file system is used, this is useful for removable devices such as CDs and DVDs.
+ **Options**:
	+ define particular options for file systems. 
	+ Some options relate only to the file system itself. 
	+ Some of the more common options are:
		+ **auto**:
			+ file system will mount automatically at boot, or when the command 'mount -a' is issued.
		+ **noauto** (no auto):
			+ the `filesystem` is mounted only when you tell it to.
		+ **exec**:
			+ allow the execution binaries that are on that partition (default). 
		+ **noexec** (no exec):
			+ do not allow binaries to be executed on the `filesystem`
		+ **ro** (read only):
			+ mount the `filesystem` read only.
		+ **rw** (read and write):
			+ mount the filesystem read-write.
		+ And [more](https://wiki.debian.org/fstab)  
+ **dump**:
	+ is used by the dump utility to decide when to make a backup. 
	+ When installed, dump checks the entry and uses the number to decide if a file system should be backed up. 
	+ Possible entries are 0 and 1: 
		+ If 0, dump will ignore the file system. 
		+ if 1, dump will make a backup.  
	+ Most users will not have dump installed, so they should put 0 for the dump entry.
+ **pass**:
	+ `fsck` reads the `<pass>` number and determines in which order the file systems should be checked. Possible entries are 0, 1, and 2. 
	+ The root file system should have the highest priority, 1, all other file systems you want to have checked should get a 2. 
	+ File systems with a `<pass>` value 0 will not be checked by the `fsck` utility.


---
# Viewing a List of Mounted File Systems


## Mount command:
+ The mount command is used to mount ﬁle systems. 
+ Entering the command without arguments will display a list of the ﬁle systems currently mounted.
>> `mount`
```
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=3865168k,nr_inodes=966292,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=781240k,mode=755,inode64)
/dev/sda2 on / type ext4 (rw,relatime,errors=remount-ro)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k,inode64)
...
/dev/sdb1 on /media/am/8S type exfat (rw,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,iocharset=utf8,errors=remount-ro,uhelper=udisks2)
...
```
+ The format of the listing is as follows:` device on mount_point type filesystem_type (options)`
+ For example `/dev/sda2 on / type ext4 (rw)`:
	+ The device is `/dev/sda2` is mounted as the root ﬁle system.
	+ The type is `ext4`
	+ And is both readable and writable (the option `rw`).


## Un mount re mount disc:
+ Unmount the disc with the `umount` command.
+ let’s unmount the disc and remount it at another location in the ﬁle system tree.
+ First unmount the disc:
	+ Use `umount` command followed by mount point of the disc.
+ Second Create new place to the disc:
	+ The next step is to create a new mount point for the disk. 
	+ A mount point is simply a directory somewhere on the ﬁle system tree. 
	+ There’s nothing special about it. 
	+ It doesn’t even have to be an empty directory.
+ Last thing re-mount the disc:
	+ Finally, we mount the CD-ROM at the new mount point. 
	+ The `-t` option is used to specify the ﬁle system type.
>> `umount /dev/sdc`
>> `mkdir /mnt/cdrom`
>> `mount -t iso9660 /dev/sdc /mnt/cdrom`


## Importance of Unmount story:
+ The problem:
	+ Computer systems are designed to go as fast as possible. 
	+ One of the impediments to system speed is slow devices. Printers are a good example. 
	+ Even the fastest printer is extremely slow by computer standards. 
	+ A computer would be very slow indeed if it had to stop and wait for a printer to ﬁnish printing a page. 
	+ In the early days of PCs (before multitasking), this was a real problem. 
+ The printer buffer:
	+ This problem was solved by the advent of the **printer buffer**, a device containing some RAM memory that would sit between the computer and the printer. 
	+ With the printer buffer in place, the computer would send the printer output to the buffer, and it would quickly be stored in the fast RAM so the computer could go back to work without waiting.
	+ you will notice that the system seems to ﬁll up memory the longer it is used. This does not mean Linux is “using” all the memory; it means that Linux is taking advantage of all the available memory to do as much buffering as it can.
+ Unmounting:
	+ Unmounting a device entails (يتضمن) writing all the remaining data to the device so that it can be safely removed. 
	+ If the device is removed without unmounting it ﬁrst, the possibility exists that not all the data destined for the device has been transferred.
	+ In some cases, this data may include vital directory updates, which will lead to ﬁle system corruption, one of the worst things that can happen on a computer.


---
# Determining Device Names


## Home of all devices:
+ If we list the contents of the `/dev` directory (where all devices live), we can see that there are lots and lots of devices.
>> `ls /dev`
+ ![[Screenshot_2023-05-10_19_06_46.png]]


## How the system names devices?
+ `/dev/fd*`:
	+ Floppy disk drives.
+ `/dev/hd*`:
	+ IDE (PATA) disks on older systems. 
	+ Typical motherboards contain two IDE connectors or channels, each with a cable with two attachment points for drives. 
	+ The ﬁrst drive on the cable is called the master device, and the second is called the slave device. 
	+ The device names are ordered such that `/dev/hda` refers to the master device on the ﬁrst channel, `/dev/hdb` is the slave device on the ﬁrst channel; `/dev/hdc` is the master device on the second channel, and so on. 
	+ A trailing digit indicates the partition number on the device. 
	+ For example, `/dev/hda1` refers to the ﬁrst partition on the ﬁrst hard drive on the system, while `/dev/hda` refers to the entire drive.
+ `/dev/lp*:
	+ Printers.
+ `/dev/sd*`:
	+ SCSI disks. 
	+ On modern Linux systems, the kernel treats all disk-like devices (including PATA/SATA hard disks, ﬂash drives, and USB mass storage devices such as portable music players and digital cameras) as SCSI disks. 
	+ The rest of the naming system is similar to the older `/dev/hd*`
+ `/dev/sr*:
	+ Optical drives (CD/DVD readers and burners).



---
# Creating New File Systems


## Sector:
+ The sector is the minimum storage unit of a hard drive.
+ Most disk partitioning schemes are designed to have files occupy an integral number of sectors regardless of the file's actual size.
+ Files that do not fill a whole sector will have the remainder of their last sector filled with zeroes. 
+ More about [disk sector](https://en.wikipedia.org/wiki/Disk_sector)


## Manipulating Partitions with fdisk:
+ `fdisk` is one of a host of available programs (both command line and graphical) that allows us to interact directly with disk-like devices (such as hard disk drives and ﬂash drives) at a very low level. 
+ With this tool we can edit, delete, and create partitions on the device.
+ To work with our ﬂash drive, we must ﬁrst unmount it (if needed) and then invoke the `fdisk` program.


## Look for our device:
+ Use amount to display a list of the ﬁle systems currently mounted and pipe the output to `grep` command with your device label:
>> `mount | grep 8S`  
```
/dev/sdb1 on /media/am/8S type exfat (rw,nosuid,nodev,relatime,uid=1000,gid=1000,fmask=0022,dmask=0022,iocharset=utf8,errors=remount-ro,uhelper=udisks2)
```


## List all disks on the device:
>> `fdisk -l`
```
Disk /dev/nvme0n1: 476.94 GiB, 512110190592 bytes, 1000215216 ....

Disk /dev/sda: 119.24 GiB, 128035676160 bytes, 250069680 
...

Disk /dev/sdb: 64 MiB, 67108864 bytes, 131072 sectors
...
```


## Make new partition:
+ First unmount the target device:
>> `umount /dev/sdb1`
+ Then use `fdisk` command:
>> `fdisk /dev/sdb`
+ Show information about the device using `i` or `p` options and for examine the existing partition layout:
```
Command (m for help): i

Selected partition 1
         Device: /dev/sdb1
           Boot: *
          Start: 2048
            End: 121307102
        Sectors: 121305055
      Cylinders: 59231
           Size: 57.8G
             Id: 7
           Type: HPFS/NTFS/exFAT
    Start-C/H/S: 0/32/33
      End-C/H/S: 1023/254/63
          Attrs: 80

Command (m for help): p
Disk /dev/sdb: 57.84 GiB, 62109253632 bytes, 121307136 sectors
Disk model: Ultra USB 3.0   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x70b20518

Device     Boot Start       End   Sectors  Size Id Type
/dev/sdb1  *     2048 121307102 121305055 57.8G  7 HPFS/NTFS/exFAT
```
+ Use `l` option to list known partition types:
```
Command (m for help): l

00 Empty            27 Hidden NTFS Win  82 Linux swap / So  c1 DRDOS/sec (FAT-
01 FAT12            39 Plan 9           83 Linux            c4 DRDOS/sec (FAT-
02 XENIX root       3c PartitionMagic   84 OS/2 hidden or   c6 DRDOS/sec (FAT-
03 XENIX usr        40 Venix 80286      85 Linux extended   c7 Syrinx         
04 FAT16 <32M       41 PPC PReP Boot    86 NTFS volume set  da Non-FS data    
05 Extended         42 SFS              87 NTFS volume set  db CP/M / CTOS / .
06 FAT16            4d QNX4.x           88 Linux plaintext  de Dell Utility   
07 HPFS/NTFS/exFAT  4e QNX4.x 2nd part  8e Linux LVM        df BootIt         
08 AIX              4f QNX4.x 3rd part  93 Amoeba           e1 DOS access     
09 AIX bootable     50 OnTrack DM       94 Amoeba BBT       e3 DOS R/O        
0a OS/2 Boot Manag  51 OnTrack DM6 Aux  9f BSD/OS           e4 SpeedStor      
0b W95 FAT32        52 CP/M             a0 IBM Thinkpad hi  ea Linux extended 
0c W95 FAT32 (LBA)  53 OnTrack DM6 Aux  a5 FreeBSD          eb BeOS fs        
0e W95 FAT16 (LBA)  54 OnTrackDM6       a6 OpenBSD          ee GPT            
0f W95 Ext'd (LBA)  55 EZ-Drive         a7 NeXTSTEP         ef EFI (FAT-12/16/
10 OPUS             56 Golden Bow       a8 Darwin UFS       f0 Linux/PA-RISC b
11 Hidden FAT12     5c Priam Edisk      a9 NetBSD           f1 SpeedStor      
12 Compaq diagnost  61 SpeedStor        ab Darwin boot      f4 SpeedStor      
14 Hidden FAT16 <3  63 GNU HURD or Sys  af HFS / HFS+       f2 DOS secondary  
16 Hidden FAT16     64 Novell Netware   b7 BSDI fs          f8 EBBR protective
17 Hidden HPFS/NTF  65 Novell Netware   b8 BSDI swap        fb VMware VMFS    
18 AST SmartSleep   70 DiskSecure Mult  bb Boot Wizard hid  fc VMware VMKCORE 
1b Hidden W95 FAT3  75 PC/IX            bc Acronis FAT32 L  fd Linux raid auto
1c Hidden W95 FAT3  80 Old Minix        be Solaris boot     fe LANstep        
1e Hidden W95 FAT1  81 Minix / old Lin  bf Solaris          ff BBT            
24 NEC DOS        

Aliases:
   linux          - 83
   swap           - 82
   extended       - 05
   uefi           - EF
   raid           - FD
   lvm            - 8E
   linuxex        - 85
```
+ Use `t` option to change a partition type.
+ Then use `w` option to save all changes.


---
# Rename the disk


## Change the disk label:
+ Use `ntfslabel` command:
>> `ntfslabel /dev/sdb1 New_disk_name`



---
# Creating a New File System with mkfs


## Make ﬁle system:
+ Use `mkfs` (short for “make ﬁle system”), which can create ﬁle systems in a variety of formats. 
+ To create an `ext4` ﬁle system on the device, we use the `-t` option to specify the “`ext4`” system type, followed by the name of the device containing the partition we want to format.
>> `mkfs -t ext4 /dev/sdb1`


## What Are File Systems?
+ File systems represent how data is stored on a storage device. 
+ They are pieces of software that help an OS organize data and use space more efficiently.
+ File systems keep everything tidy and minimize loss of storage space by logically organizing data.
+ More about [file system](https://www.makeuseof.com/ntfs-fat-exfat-windows-10-file-systems-explained/).



---
# Testing and Repairing File Systems


## File system table file again:
+ In our earlier discussion of the `/etc/fstab` ﬁle, we saw some mysterious digits at the end of each line. 
+ Each time the system boots, it routinely checks the integrity of the ﬁle systems before mounting them. 
+ This is done by the `fsck` program (short for “ﬁle system check”).


## File system check:
+ In addition to checking the integrity of ﬁle systems, `fsck` can also repair corrupt ﬁle systems with varying degrees of success, depending on the amount of damage. 
+ On Unix-like ﬁle systems, recovered portions of ﬁles are placed in the lost+found directory, located in the root of each ﬁle system.
>> `fsck /dev/sdb1`


---
# Show partitions on each disk


## Parted command:
+ `parted` command with `-l` option will list all disks in the device and show errors on disk if exists.
>> `parted -l`
```
Model: ATA SAMSUNG MZ7PD128 (scsi)
Disk /dev/sda: 128GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End    Size    File system     Name  Flags
 1      1049kB  538MB  537MB   fat32                 boot, esp
 2      538MB   127GB  126GB   ext4
 3      127GB   128GB  1024MB  linux-swap(v1)        swap


Error: /dev/sdb: unrecognised disk label
Model: SanDisk Anisha (scsi)                                              
Disk /dev/sdb: 67.1MB
Sector size (logical/physical): 512B/512B
Partition Table: unknown
Disk Flags:
```



---
# Moving Data Directly to and from Devices


## Data deﬁnition (dd) program:
+ If we could treat a disk drive as simply a large collection of data blocks, we could perform useful tasks, such as cloning devices.
+ The `dd` program performs this task. It copies blocks of data from one place to another. 
+ It uses a unique syntax (for historical reasons) and is usually used this way: 
	+ `dd if=input_file of=output_file [bs=block_size [count=blocks]]`


## Mirror two flash drives:
+ Let’s say we had two USB ﬂash drives of the same size and we wanted to exactly copy the ﬁrst drive to the second. 
+ If we attached both drives to the computer and they are assigned to devices `/dev/sdb` and /dev/sdc, respectively, we could copy everything on the ﬁrst drive to the second drive with the following:
>> `dd if=/dev/sdb of=/dev/sdc`
+ Alternately, if only the ﬁrst device were attached to the computer, we could copy its contents to an ordinary ﬁle for later restoration or copying:
>> `dd if=/dev/sdb of=flash_drive.img`



---
# Checksum


## MD5 sum:
+ A checksum is the result of an exotic mathematical calculation resulting in a number that represents the content of the target ﬁle.
+ If the contents of the ﬁle change by even one bit, the resulting checksum will be much different. 
+ The most common method of checksum generation uses the `md5sum` program.
>> `md5sum image.iso`
`34e354760f9bb7fbf85c96f6a3f94ece   image.iso`
+ After you download an image, you should run `md5sum` against it and compare the results with the `md5sum` value supplied by the publisher.



