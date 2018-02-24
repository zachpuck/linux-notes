# swap disks

list disk to find which are listed as swap
`fdisk -l /dev/sdb` 

`mkswap /dev/sdb5` - setting up a swap

`swapon -s` -> summary of swap devices being used

`swapon /dev/sdb5` -> enables swap on sdb5 device

`swapoff /dev/sdb5` -> turning swap off
`swapoff -a` -> disable all swap

`free -m` -> show the swap space being used, free, and total. 

### configure priority and mounting for swap

vim /etc/fstab
`uuid="<id of swap if a partition>" swap swap sw, pri=5 0 0`

the higher priority is the one with the higher number. 