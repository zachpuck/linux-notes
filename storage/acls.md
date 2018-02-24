# extending permissions with ACLs

### list ACL support
find file and kernel support details

`ls /boot/config-*` -> lists kernel config files.

`uname -r` -> list kernel version to match up result of above.

`grep ACL /boot/config-$(uname -r)` -> see the levels of ACL support.
l = directly in the kernel
m = compiled as a module

`sudo tune2fs -l /dev/sdb6 | grep -i default` -> this will show if the default options are using acl.

### display ACL
`ls -l` the dot at the end of the permissions shows acl support but not set. if it is a + symbol this means that the acl is set

`getfacl <filename>` -> get acl details of a file

### configure default ACLs
`mkdir test-acl`
`ls -ld test-acl/`
`getfacl test-acl/`
`umask`
`setfacl -m d:o:--- test-acl/` -> set default acl for other users to nothing
`!get` -> we see that now we have added entries for default

`touch test-acl/file1`
`ls -l test-acl/file1` -> no other permissions are set now
`ls -ld test-acl/` -> we now see the acl attribute is set with a '+'. 

`setfacl -dm u:bob:rw test-acl` -> bob now has read and write on the files in the test-acl dir.
`touch test-acl/file2`
`getfacl test-acl/file2` -> we can see bob is listed with read and write permissions. 

### add additional ACE
access control entries

`mkdir /work`
`ld -ld /work`
`chmod o= /work` -> set others permissions to nothing on work dir.
`setfacl -m u:bob:rx /work/`
`getfacl /work` -> bob now has read and execute on work dir

### removing ACLs
`setfacl -x u:bob:r /test-acl/file2` -> remove entry for bob on file one.

`setfacl -b file1` -> removes the entry acl list (`ls -l` will now show a '.' instead of '+')

### diagnose and correct file access issues

`ls -l /etc/shadow`
`chage -l bob`
`chcon -t admin_home_t /etc/shadow`
`chage -l bob`
`ls -Z /etc/shadow`
`ausearch -m AVC -ts recent`
`restorecon /etc/shadow`
`!cha`

web server example with httpd installed
`mkdir /web`
`chgrp apache /web`
`chmod 2750 /web`
`setfacl -m d:o:--- /web`
`echo "Test Web" > /web/index.html`
`ls -l /web/index.html`
`vim /etc/httpd/conf/httpd.conf`
change DocumentRoot "/web"

apachectl configtest
`systemctl restart httpd`

`ausearch` -> shows the wrong context set
`semanage fcontext -a -t httpd_sys_content_t "/web(/.*)?"`
`restorecon /web`
`restorecon /web/*`
`ls -Zd /web/`

