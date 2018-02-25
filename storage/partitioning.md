lsblk - list all block devices
# partitioning

| Linux File System Overview ||||
|---|---|---|---|
| File System: ext2, ext3, ext4, XFS, ... ||||
|Logical Partitions \| Primary Max 4|||Partition Max 128|
|MBR Partition Table 2TB|||GUID Partition Table 8ZB|||
|DISK||||

DOS Label:
- maximum 2TB partition size
- 4 Primary partitions (1 extended)
- manage with fdisk
- default type: 83 Linux
- additional type:
    - 82 swap
    - 83 LVM
    - fd RAID

GPT Label:
- Maximum 8ZB partition size
- 128 Partitions (hardware drives limit this)
- manage with gdisk
- types:
    - 8300 Linux
    - 8200 Swap
- Copy held at end of the disk for backups

### fdisk
partitioning disks with fdisk

`fidsk -l /dev/sdb` -> list out partitions

`fdisk /dev/sdb` -> navigate into the fdisk tool

You can click `m` to see the menue and available options

`w` -> save

`ctrl` + `C` - exists without saving 


we can now list fdisk and see that any we created no longer exist.

### gdisk
partitioning disks that support GPT (GUID partition tables)

`gdisk /dev/sdb` -> looks for any parition tables, if none found it creates one and goes into the gdisk tool. 

`?` to view menu

`gdisk -l /dev/sdb` -> list out the partitions on disk

the end of the disk is reservered for a backup of the GPT table. this will allow you to restore the table if it gets corrupt. 

### parted
works with MBR and GPT and works with commandline for scripting

`parted /dev/sdb print` -> partition table information

`parted` -> to enter the parted tool

`mklabel msdos` -> to create/change the partition table, you can change it at any time with the same command.

`mkpart primary 1 200` -> creating primary partition from 1 to 200 mb

`print` or `p` -> show the new partition just created

`quit` -> to exit

#### scripting with parted

```
#!/bin/bash
DISK="/dev/sdb"
# Create MBR partition table and extended partition across disk
parted -s $DISK -- mklabel msdos mkpart extended 1m -1m

#Create swap partition as partition 5 the first logical parition
parted -s $DISK mkpart logical linux-swap 2m 100m #5

parted -s $DISK mkpart logical 101m 200m #6
parted -s $DISK mkpart logical 201m 300m #7
parted -s $DISK mkpart logical 301m 400m #8
parted -s $DISK mkpart logical 401m 500m #9

#Create 3 more logical partitons for LVMs
parted -s $DISK mkpart logical 501m 600m #10
parted -s $DISK mkpart logical 601m 700m #11
parted -s $DISK mkpart logical 701m 800m #12
parted -s $DISK set 10 lvm on # set partition 10 to LVM
parted -s $DISK set 11 lvm on # set partion 11 to LVM
parted -s $DISK set 12 lvm on # set partition 12 to LVM

#Create 2 more partions for RAID
parted -s $DISK mkpart logical 801m 900m #13
parted -s $DISK mkpart logical 901m 1000m #14
parted -s $DISK set 13 raid on # set partition 13 to RAID
parted -s $DISK set 14 raid on # set partion 14 to RAID
parted -s $DISK print
```

continue to use `lsblk` to see all the new partitions created

delete the partition table: 
`dd if=/dev/zero of=/dev/sdb count=1 bs=512` 

backup a partition:
`dd if=/dev/sda count=1 bs=512 of=/root/sdb.mbr` 

if -> input file
of -> output file