`ssh -f -L 8080:localhost:80 user@server2 -N`
-> listening on localhost 8080 to port 80 via ssh to server2

`ps -ef | grep ssh`
`kill <id of ssh tunnel>` -> this will disconnect the above ssh tunnel

### openvpn
`yum install openvpn easy-rsa -y`

`systemctl stop firewalld`
`iptables -L`
`iptables -L -t nat`
to verify no firewall rules are running.

add masquerade rule
`iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`

sample vpn file located under docs:
/usr/share/doc/openvpn-2.3.11/sample/sample-config-files/server.conf

using **easy-rsa** to setup the certificate and keys
the scripts can be copied from /usr/share/easy-rsa/2.0/* to /etc/openvpn/easy-rsa

