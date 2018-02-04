# accessing the root account

### su
requires you to know the password of the user

`su` => access as root user, prompts for password

`su -l` => new shell as the user including environment echo $USER

`su testuser` => login as testuser

### sudo

`sudo cat /etc/sudoers` => see who has permission to run sudo

`sudo visudo` => how you edit the sudoers file.

soduer file
% => group reference
ALL=(root) ALL => connecting from anywhere allow all commands as root.

setting up a customer set of commands that a group can run:

1. User_Alias HELPDESK = joe, sally
2. Cmnd_Alias HELPCOMMANDS = /usr/sbin/useradd, /usr/bin/passwd
3. HELPDESK ALL=(root) HELPCOMMANDS

### restricting root access via SSH

vim /etc/ssh/sshd_config
update: PermitRootLogin `no` on centos

