# Logical volumes

### creating logical volumes
pvscan -> look for physical volumes
vgscan -> volume group list
lvscan -> logical volumes

fdisk -l /dev/sdb

pvcreate /dev/sdb10
pvcreate /dev/sdb11

vgcreate vg1 /dev/sdb10 /dev/sdb11 -> create volume group

vgscan
vgs -> more info

lvcreate -n lv1 -L 184m vg1 -> create logical volume on vg1 volume group.

lvscan -> will show the newly created lvm

mkfs.xfs /dev/vg1/lv1 -> create the file system on this new logical volume

add it to the fstab file.
mkdir /lvm

vim /etc/fstab
/dev/vg1/lv1 /lvm xfs defaults 0 0

mount -a 

mount -> we now see our device in /lvm location

find /usr/share/doc -name '*.pdf' -exec cp {} /lvm \; -> find all pdfs in doc dir to lvm location

checking space
df -h

### resizing lvm
in case of low space
extend the logical volume structure
`df -h /lvm`
`pvscan` -> use another physical volume in lvm

`vgextend vg1 /dev/sdb12`
`vgs`
`lvextend -L +50m /dev/vg1/lv1`
`xfs_growfs /lvm` -> resize file system while online (`resize2fs` for ext4 file systems)
`df -h /lvm` -> will now show increased size

### lvm snaphsots
`lvcreate -L 30m -s -n backup /dev/vg1/lv1`
-s -> snapshot

mounting the snapshot
`mount /dev/vg1/backup /mnt -o nouuid,ro`
`ls /mnt`

`tar -cf /root/backup.tar /mnt`
`umount /mnt`
`lvremove /dev/vg1/backup`

### migrating Phyiscal Volume
create the new physical volume using fdisk

pvcreate /dev/sdc5
vgextend vg1 /dev/sdc5
pvmove -b /dev/sbd10 /dev/sdc5 -> (background) move data from sb10 to sdc5

reduce size
vgreduce vg1 /dev/sbd10
pvremove /dev/sdb10

vgs
vg1 has free data now

