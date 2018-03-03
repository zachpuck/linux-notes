# firewalling with firewalld

`firewall-cmd --state`
`systemctl start firewalld.service`

`firewall-cmd --get-default-zone`
`firewall-cmd --get-active-zones`
`firewall-cmd --get-zones`

`firewall-cmd --permanent --zone=public --remove-interface=enp0s3`

`firewall-cmd --permanent --zone=external --add-interface=enp0s3`

`systemcl restart firewalld.service`

`firewall-cmd --set-default-zone=external`

### service and port rules

`firewall-cmd --list-all`
`iptables -L`

remove ssh from external and then reload
`firewall-cmd --permanent --zone=external --remove-service=ssh`
`firewall-cmd --reload`

listing all the services for a specific zone
`firewall-cmd --list-services --zone=external`

`ls /usr/lib/firewalld/services/`

create new service
`firewall-cmd --permanent --new-service="puppet"`
we will now see the new service file in /usr/lib/firewalld/services/puppet.xml. 
to adjust the permissions on the new firewall service
`restorecon puppet.xml`
`chmod 640 puppet.xml`
`vim puppet.xml`
> <port protocol="tcp" port="443"/>
`firewall-cmd --permanent --add-service=puppet --zone=internal`

### masquerading
`firewall-cmd --permanent --remove-masquerade --zone=external`
`firewall-cmd --permanent --add-masquerade --zone=external`