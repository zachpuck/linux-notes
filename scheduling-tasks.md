# scheduling tasks in linux

### cron jobs

ls /etc/cron*

/etc/crontab - system location for cron jobs

setting up system cronjobs as root
`vim /etc/crontab`
`vim /etc/cron.d` -> put files in the crontab format to be run as well. 

insert new entry
`30 8-18 * * 1-5 root df -h` -> every 30 minutes from 8 am to 6 pm monday through friday

user crons
`crontab -l` -> list crons
`crontab -e` -> edit cron jobs
`crontab -r` -> remove crontab file

### anacron
cat /etc/anacrontab

`vim /etc/anacrontab`
1 45 backup tar -cf /tmp/backup /etc

### checking status
`systemctl status crond`
`ls /etc/cron.hourly`

### At daemon
once off jobs

`systemctl status atd` -> check status of At daemon

schedule a job
`at noon`
at> `ls /etc`
at> `ls /tmp`
at> `<EOT>`

see schedule jobs in queue
`atq`

remove a job
`atr <number from atq>`

specific date to schedule the job
`at 13:24 jun 23`

### denying permission to run at or cron jobs
ls /etc/*.deny
