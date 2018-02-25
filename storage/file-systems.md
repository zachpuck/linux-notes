### formatting EXT4 File Systems

fdisk -l /dev/sdb -> list our partitions and pick the partition to work with.

`mkfs.` (hit tab to see all the file system types you can choose from.)

`mkfs.ext4 -L dataDrive /dev/sdb6` -> create file system with label

`tune2fs -L MyData -c 0 -i 0 /dev/sdb6` -> changing details of a filesystem

`dumpe2fs /dev/sdb6 | less` -> output file system details. 

### Formatting XFS file system
default system on centos7

`mkfs.xfs -b size=1k -l size=10 /dev/sdb7`

-b -> block size
-l -> transaction log

`xfs` -> hit tab to see available commands

`xfs_db -x /dev/sdb7` -> to access to management tool, '-x' allows for modifying
`help` -> see all the options inside of the xfs_db

`uuid` -> output the uuid of the file system
`label DATA2` -> set new label


### mounting file systems
`mount /dev/sdb6 /mnt` -> mounting a file system

`umount /mnt` -> to remove a file mount

`mkdir -p /data/{mydata,data2}` -> make new directories under /data patch of root file system. 

we can now mount a file system into these directories
`mount /dev/sdb6 /data/mydata`

`mount | grep mydata` -> search for a directory details

`mount -o remount,noexec /dev/sdb6 /data/mydata` -> setting some options on a file system, (no executables, so data only).

`umount /data/mydata` or `unmount /dev/sdb6` -> unmount the filesystems.

we can also see all mounted file systems under `cat /proc/mounts`

#### to persist a mount
"/etc/fstab" file

`blkid /dev/sdb6` -> get unquie Id of file system
`vim /etc/fstab` -> edit the file 
`G` -> vim command to go to last line
`o` -> insert new line
paste in uuid from blkid cmd (), mount point, file type, options, dumpfile, file system check (only applies for ext file systems)
`UUID="<id goes here>" /data/mydata ext4 noexec 0 2`

`mount -a` -> automount all files

review mount options in manual
`man mount`
search ("/") for "ext4", "INDEPENDENT", and "xfs"

noexe, noatime, uquota

