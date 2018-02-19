# SELinux/AppArmor

`ls -Z /etc/shadow` -> selinux user, role, type

`getenforce` -> see current mode
`sestatus` -> details about the current SELinux settings

`cat /etc/selinux/config` -> set mode and type 

`setenforce 0` -> changes the mode to Permissive

`id -Z` -> shows the users selinux settings
`ps -Z` -> shows services and their context/type for selinux

### SELinux logs
`tail /var/log/audit/audit.log` -> all the audit logs

`ausearch -m avc` -> search the selinux logs using acess vector control module

`ls -Z /etc/shadow`

`chcon -t unlabeled_t /etc/shadow` -> change the label/context of the shadow file. this will cause access denied

`ausearch -m avc -ts recent` -> search recent logs and see the failed loggin due to the 'unlabeled setting above. 

`restorecon /etc/shadow` -> restores the shadow file from master

`semanage fcontext -l | grep /etc/shadow`

`ls /etc/selinux/targeted/contexts/files`

