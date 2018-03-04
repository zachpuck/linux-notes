# hostnames

to list the hostname
`echo $PS1`
`hostname` or `hostname -f` -> full name
`uname -n`

### hostnamectl
change hostname
`hostname centos7`
if you reboot it would reset

`cat /etc/hostname` -> set here to make it persistent

`hostnamectl set-hostname centos72.example.com` -> this will set it perminently.

setting a pretty name put `"` around the hostname when using `set-hostname`

`cat /etc/machine-info` -> stores pretty name information

### name resolution
`cat /etc/hosts`

to add alias you can add them to the end of the line.
order:
IP, FQDN, alias

#### dns
`getent hosts`
grep hosts /etc/nsswitch.conf -> control the order of name resolution

`cat /etc/resolv.conf`

`yum install -y bind-utils`
`dig www.google.com` -> find out dns information about a domain

`dig www.google.com @8.8.8.8` -> set the server to check from

`dig +short www.google.com`

`dig google.com MX` -> find out mx details

