**High Availability Cluster**: HA Clusters can manage resources such as websites and migrate the resource to another node in the event of a failure or planned downtime.

### Pacemaker 
`yum install pacemaker pcs resource-agents` -> main ha software

`echo 'hacluster:Password1' | chpasswd`

#### enable firewall ports
ports: TCP 224, 3121, 21064, and UDP 5405

`firewall-cmd --permanent --add-service=high-availability`
`firewall-cmd --reload`

### configuring cluster
`systemctl enable pcsd`

`pcs cluster auth server1.example.com server2.example.com -u hacluster -p Password1` -> authorize the nodes

`pcs cluster setup --name cluster1 server1.example.com server2.example.com` -> create cluster

`pcs cluster start --all` -> start up the cluster

`pcs status` -> we can see the servers online.

`systemctl enable corosync pacemaker` -> enable the services to start at startup.

### Disable STONITH and Quorum 
if a device fails we want to make sure if it comes back it does not look at the system.
`pcs property set stonith-enabled=false`

Quorum is ideal for odd number of nodes (3 / 5/ 7)

`pcs property set no-quorum-policy=ignore` -> since only 2 nodes atm

`less /etc/corosync/corosync.confg` -> to see these settings, use the pcs commands to write to this file. 

### clustered resources
cluster IP address
`pcs resource create cluster_ip ocf:heartbeat:IPaddr2 ip=192.168.1.55 cid_netmask=24 op monitor interval=20s`

`pcs status` -> now shows cluster ip

`pcs cluster standby server1.example.com` -> gracefully set machine to unavailable (`unstandby` to bring it back)

