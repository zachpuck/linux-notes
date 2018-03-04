# iptables

list
`iptables -L`

`iptables-save > fwoff` -> save the config to the fwoff file

`iptables -A INPUT -i lo -j ACCEPT`
-> accept any traffic from local interface

`iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT` -> if we establish a connection the traffic wil be able to come back.

`iptables -A INPUT -p tcp --dport 22 -j ACCEPT` -> allowing traffic on port 22 in.

`iptables -L` will now list these new rules
`iptables -nvL`

`iptables-save > fwon`
`iptables-restore < fwoff`

`iptables -A INPUT -j DROP` -> only allowed traffice is going to be allowed in now.

`iptables -F` -> flush all the rules

### managing iptables via a service
`yum install -y iptables-services`

`vim /etc/sysconfig/iptables`-> rules be read in to service
`vim /etc/sysconfig/iptables-config` -> can configure the service to save the settings on a restart or stop. 

`systemctl enable iptables.service`

`iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT` -> inserts in config as first rule



