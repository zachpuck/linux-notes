# Configuring an iSCSI Block Storage

**iSCSI Target**: iSCSI targets share block devices, often LVMS, to clients known as iSCSI initiators over the LAN.

### installing iSCSI Target and setup firewall

`yum install targetd targetcli`

`systemctl enable targetd`

`firewall-cmd --add-service=iscsi-target --permenent`

`firewall-cmd --reload`

`firewall-cmd --list-services`

this opens port 3260

### creating LVM to share

vgs
`lvcreate -L 100m -n web_lv vg1`
`lvscan`

### configure iSCSI Target
`targetcli`

inside of targetcli you have multiple cmds

`ls`
`backstores/block create web_store /dev/vg1/web_lv`
`ls`
`iscsi/ create iqn.2018-02.com.example.server1:web` -> target unique name

`cd iscsi/iqn ../web/tpg1`
`luns/ create /backstores/block/web_store`

`acls/ create iqn.2018-02.com.example.server2:web` -> identified the client to the server

`exit`

`netstat -ltn` -> listenting on port 3260.

### configure the client (iSCSI initiator)
`yum list available | grep iscsi`
`yum install iscsi-initiator-utils`

`iscsi` (hit tab) -> multiple commands available

`vim /etc/iscsi/initiatorname.iscsi`
InitiatorName=iqn.2018-02.com.example.server1:web

`iscsiadm --mode discovery --type sendtargets --portal server1.example.com --discover`

`iscsiadm --mode node --targetname iqn.2018-02.com.example.server1:web --portal server1.example.com --login`

