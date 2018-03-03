# Routing

`ip route show` -> show ip route table
`route`
`netstat -nr`

`ip route add default via 192.168.1.104` -> this would default route all requests to this ip

### setting up a router
enabling routing

`cat /proc/sys/net/ipv4/ip_forward` -> default value of 0 means forwarding is turned off

`vim /etc/sysctl.conf`
>net.ipv4.ip_forward=1

`sysctl -p` to read in change

### enabling NAT

`systemctl stop firewalld`
`iptables -L` 

enable nat
`iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`

`iptables -t nat -L` -> now shows the masquerade entry
