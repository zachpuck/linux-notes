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


