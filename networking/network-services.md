# ip

`ip addr`
`ip -4 a` -> ip v4 only

`ip addr add 172.17.55.3/16 dev enp0s8` or `ip a a`(shorthand) -> add an ip to the device enp0s8

### NetworkManager
`systemctl status NetworkManager` (note case)

`nmcli connection` (double tab to show all options)
options:
add
delete
down
show
-p -> pretty format option

`nmcli -p connection show`

`nmcli connection add con-name home ifname enp0s8 type ethernet ip4 192.168.1.88 gw4 192.168.1.1`

`ip addr show enp0s3` -> show only for this interface

### network service
bridging and more advance network configurations

`systemctl status network`
`ls /etc/sysconfig/network-scripts`
NM_CONTROLLED=no -> setting in a network script to prevent NetworkManager from controlling the interface

`ifup` -> bring up a network interface
`ifdown` -> bring down a network interface