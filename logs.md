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

