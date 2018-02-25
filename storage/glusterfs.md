**GlusterFS**
The GlusterFS Service allows you to create replicated, striped and distributed filesystem across nodes on your network

install latest glusterfs-server

`firewall-cmd --permanent --add-service=glusterfs`

create directorys on the mounted volumes (ex: /gfs/data1)

`gluster peer probe server2.example.com`

`gluster peer status`

`gluster volume create volume1 transported tcp server1.example.com:/gfs/data1 server2.example.com:/gfs/data1`

`gluster volume start volume1`

`gluster volume info`

`mount -t glusterfs server1.example.com:/volume1 /mnt` -> mounting the created gluster volume

we can now save files that will be spread out across both servers (transported).

#### replicate data
mkdir /gfs/repdata

`gluster volume create vol_replicated replica 2 server1.example.com:/gfs/repdata server2.example.com:/gfs/repdata`

`gluster volume start repdata`

now when we mount this volume and save files in this 'repdata' volume the data will be mirrored to both servers. 
