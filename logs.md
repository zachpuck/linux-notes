# log files and log rotation

## auditing login events
`lastlog` every user even if they have not logged in

`lastlog | grep -v "Never"` -> -v rervise the search, lines that done contain 'never'

`last` -> reading from log file /var/log/wtmp

`last -n 10` to see just the last 10 lines

`last | grep "still"` -> all users still logged in

`last reboot` -> all the reboots of the system

`last <user>` -> specific users activity

`sudo lastb` -> last bad login attempts (failed passwords)

## auditing root access
su and sudo

`ls /var/log/secure*`

`less secure` -> secure events like policy, su, and sudo

`grep sudo /var/log/secure*` -> look for sudo events in all of the secure log files

## scripting with awk
`tail -n 1 /var/log/secure`

`awk '/sudo/ { print $0 }' secure` -> search the secure file for lines containing sudo

to print out just field five: space seperated
`awk '/sudo/ { print $5 }' secure`
`awk '/sudo/ { print $5, $6, $14 }' secure`

`vim secure.sh`
```
#!/sur/bin/bash
awk "/$1/ { print \$5,\$6,\$14}" $2
```
to run the script
`./secure.sh su: /var/log/secure` -> looks for the su events ($1) in the file provided ($2). and prints out the fields 

## system logging daemons

`ls /etc/rsyslog*`

rsyslog.conf -> improves on the standard syslog daemon

`vim rsyslog.confg`
under RULES you can see where some of the information is logged

adding our own rule:
`local1.info    /var/log/testlog`
restart daemon `systemctl restart rsyslog`

adding test log
`logger -p local1.warn "test message"`
`tail /var/log/messages` -> we see the file, as everything is logging here.
`tail /var/log/testlog` -> we also see it goes here. 

## rotating log files
a daily cron will run to do `logrotate`
`ls /etc/cron.daily`

`less /etc/logrotate.conf` -> control the log rotation schedule
adding a rotation
`vim /etc/logrotate.conf`
```
/var/log/testlog {
    missingok
    notifempty
    size 10
    compress
}
```

`ls /var/log/testlog`
`logrotate /etc/logrotate.conf`
`ls /var/log/testlog` -> we now see the rotated file as well.

## systemd and journalctl
`journalctl` -> reading from a unified log

`journalctl -n` -> last 10 entries

`journalctl -f` follow the log

creating additional boot records/logs
`mkdir /var/log/journal`
`vim /etc/systemd/journald.conf`
change `Storage=auto` to `Storage=persistent`

`journalctl -u sshd.service` -> shows only information passed in from the sshd service

`journalctl --since "2018-01-21 11:15:00"` -> shows everything since 11:15 on jan 21

`journalctl --since "10 minutes ago"` -> shows everything in the last 10 minutes

`journalctl --list-boots` -> if persistant storage is enabled this will show all the journal files, one for each reboot
`journald.confg` controls the number of logs we keep

