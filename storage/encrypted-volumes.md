**LUKS**: Linux Unified Key Setup is the default mode for encrypting volumes in CentOS 7

`lvcreate -L 60m -n enc /vg1`

`shred -v --iterations=1 /dev/vg1/enc` -> Shredding the volume or partition first ensures that it is full of random data. In this way the complete volume is encrypted as it all contains data.

`grep -i DM_CRYPT /boot/config-$(uname -r)` -> m = supported by a module

`lsmod | grep dm_crypt` -> it is not loaded by default but will be loaded if it is used

`modprob dm_crypt` -> to load the module manually. 

`cryptsetup -y luksFormat /dev/vg1/enc`
enter passphrase

`cryptsetup luksDump /dev/vg1/enc`

`cryptsetup luksOpen /dev/vg1/enc enc_vol` -> open device

`ls /dev/mapper` -> enc_vol is now mapper

`mkfs.ext4 /dev/mapper/enc_vol` -> creating the file system

`cryptsetup luksClose enc_vol` -> close the encrypted volume

blkid -> get uuid of volume
`vim /etc/crypttab` -> 'luks-data UUID=<id from above ste>'

`vim /etc/fstab` -> '/dev/mapper/luks-data /luks-data ext4 default 0 0'


