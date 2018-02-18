reboot
halt
poweroff

shows some legacy init daemon commands (use systemctl instead)
`init --help`

shutdown system with halt in 10 minutes
`shutdown -h 10 "the system goes offline in 10 m"`

cancel shutdown
`shutdown -c`

`cat /run/nologin` gets created at the 5 minute mark to prevent anyone not root from logging in. 

accessing a system as single user mode for troubleshooting (run level 1)
`systemctl isolate rescue.target`

### booting
to edit the boot  you can choose "e" and on the "linux16" line you can add "systemd.unit-rescue.target" this will boot in single user mode.

see what run level you are running in
`who -r`

### editing grub file
`vim /etc/default/grub`
`shift + g` to go to the bottom line and `shift + a` to go to the end of the line.

you can enabling recovery mode edit the last line to be false
`GRUB_DISABLE_RECOVERY="false"`
now update the grub config
`grub2-mkconfig -o /boot/grub2/grub.cfg`

a new entry will show in grub boot for recovery mode

### reset lost root password in centos7
e to edit
on linux16 entry
remove `quiet` and `rhgb` from the end of the line
add `rd.break` `enforcing=0`
remount root file system
`mount -o remout,rw /sysroot`
`chroot /sysroot`
`passwd` ; exit
now we can enter a new password
`mount -o remout,ro /sysroot` ; exit
login as root with new password
`restorecon /etc/shadow`
`setenforce 1` 

## managing GRUB2
reinstall GRUB2
`grub2-install /dev/sda` (it could be a different device depending on system)

editing grub file
`vim /etc/default/grub`

updating the grub file after changes
`grub2-mkconfig -o /boot/grub2/grub.cfg`

changing complex settings with `grubby` tool
`grubby --default-kernel`
`grubby --set-default /boot/vmlinuz-...`
`grubby --info=ALL`
`grubby --info /boot/vmlinuz-3...`

`grubby --remove-args="rhgb quiet" --update-kernel /boot/vmlinuz-3...`

### password protect GRUB2
`cp /etc/grub.d/01_users .`
`vim /etc/grub.d/01_users`
removed everything but superusers
add `password <name> <pass>`

`ctrl + r` to search histroy

encrypt the password
`grub2-mkpasswd-pbkdf2`
returns a hash
edit config again `vim /etc/grub.d/01_users`
replace `password_pbkdf2 <name> <encrypt pass hash>`

custom GRUB2 Entries
`vim /etc/grub.d/40_custom`
