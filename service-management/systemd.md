`ps -fp 1` -> shows systemd

`systemctl status sshd` -> details of the sshd service

`systemctl s` (doulbe tab to see options that start with s)
`systemctl status s` (list services that start with s)

this is done with bash-completion module installed
`yum install -y bash-completion`

`systemctl mask sshd`  -> this prevents the server from being started again if it is stopped, other admins will see a warning to indicate there is a reason it was stopped or disabled.
