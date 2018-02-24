# Managing software RAID

**Linear**: Partitions/disk not the same size, volume is expanded across all disks in array. Spare disk is not support.

**RAID0**: Similar to above but the disks or partitions are of similar size.

**RAID1**: Mirror data between devices of similar size.

**RAID4/5/6**: Three or more devices (4 with RAID6), data is stripped with parity.

### setting up a raid

`cat /proc/mdstat` -> shows any setup raid devices

`mdadm` - Multi Disk Administration

create a raid device of 2 disk
`mdadm --create --verbose /dev/md0 --level=mirror --raid-devices=2 /dev/sdb13 /dev/sdb14`

`ls -l /dev/md0` (block device file is created)

`lsmod | grep raid` -> see the driver in use

`mkfs.xfs /dev/md0` - creates the file system on the new raid.

`mdadm --detail --scan` -> get details of how the raid array is setup. 

we need to add the above details to the configure for startup
`mdadm --detail --scan >> /etc/mdadm.conf`

`mdadm --stop /dev/md0` -> stop the raid array

`mdadm --assemble --scan` -> reading information in from /etc/mdadm.conf file. 
