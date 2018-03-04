# BIND DNS

BIND -> Berkely Internet Name Domain. The most widely implemented Domain Name System (DNS) service.

### BIND
yum install -y bind bind-utils

`systemctl enable named` -> bind service name

### DNS Forwarding
`netstat -ltn` -> port 53 we are only listening on the localhost

config: `vim /etc/named.conf`
to listen on any port
>listen-on port 53 { any; };
to set which networks are allowed to query the server
>allow-query { localhost; 192.168.1.0/24; localnets; };
forwarding requests
>forwarders { 8.8.8.8 };
>forward only;

`named-checkconf -v` -> verbose verify config is good

`systemctl restart named`

### DNS Files and Locations
/etc/named.conf 
see directory in the conf file
>directory "var/named";

log file "data/named.run" -> relative path based on directory path. 

zones files
/etc/named.rfc1912.zones

`ls -l /var/named`

### zones
`vim /etc/named.conf`

referencing a zone in named.conf file:
```
zone "example.test." {
    type master;
    file "db.example";
    allow-update { none; };
};
```

#### creating a zone file
cd /var/named
cp named.empty db.example
chgrp named db.example
vim db.example

```
$TTL 3H
$ORIGIN example.test.
example.test. IN SOA server1.example.test. root.example.test. (
    1       ; serial
    1D      ; refresh
    1H      ; retry
    1W      ; expire
    3H )    ; minimum
example.test.   NS  server1.example.test.
server1         A   192.168.1.110
```

`named-checkzone example.test db.example` -> verify conf is correct

`systemctl restart named` -> restart

`cat /var/named/data/named.run` -> check logs

### DNS Queries using Python
yum install python-dns

vim /usr/shar/doc/python-dns-v1/examples/mx.py

setting our own python script to return resolver data
```
#!/usr/bin/env python 

import dns.resolver
r = dns.resolver.Resolver()
r.nameservers = ['127.0.0.1']
answers = r.query('example.test', 'NS')
for rdata in answers:
    print rdata
```
