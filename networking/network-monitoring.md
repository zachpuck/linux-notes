`tracepath www.google.com` -> shows the path

`ip link show` -> shows MAC address

`ip -s link show` -> shows statistics 
RX - Receive
TX - Transmit

### netstat
`netstat -tln` -> show tcp ports listening and port number rather than name. 

`netstat -i` -> list interfaces

`netstat -s` -> ip stack statistics

### sysstat
`ls /etc/cron.d` -> should see a sysstat file

`ls /var/log/sa` -> showing all the sysstat files

`sar -n DEV` -> n for network, for today.

`sar -n DEV 1 1` -> reading realtime

`sar -n DEV 1` -> will be monitoring in real time and showing the traffic

### nmap
yum install nmap

`nmap scanme.nmap.org` -> check which ports are open

`nmap -iflist` -> list of interfaces and ip address and route table

