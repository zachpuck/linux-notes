# time

`date`
`hwclock` - hardware clock ( when system shutdowns it runs `hwclock --systohc`)

`timedatectl` -> sets date and hwclock together. it is configured by default to automatically update time via ntp

### chrony
time synchronization

`yum install -y chrony`

`vim /etc/chrony.conf` - configuration file
`systemctl enable chronyd`
`systemctl start chronyd`

`chronyc tracking` 
`chronyc sources` -> what sources we are syncing to

### network time protocol
used udp port 123 - sames as chryonyd so only one should be runing at a time. 

`vim /etc/ntp.conf` -> configuration file
`systemctl start ntpd`

`ntpq -p` -> list servers sychronizing with
