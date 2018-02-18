# monitoring linux performance
### standard tools in procps-ng
list all programs included in pkg
rpm -ql procps-ng | grep '^/usr/bin/'

cound them 
rpm -ql procps-ng | grep '^/usr/bin/' | wc -l

```
/usr/bin/free
/usr/bin/pgrep
/usr/bin/pkill
/usr/bin/pmap
/usr/bin/ps
/usr/bin/pwdx
/usr/bin/skill
/usr/bin/slabtop
/usr/bin/snice
/usr/bin/tload
/usr/bin/top
/usr/bin/uptime
/usr/bin/vmstat
/usr/bin/w
/usr/bin/watch
```

### review memory
`free`
`free -m` - in mb

### pwdx and pmap
`pmap <pid>` shows memory map of a process

`pwdx <pid>` or `pwdx $$` - shows the directory the process is workign with.

this looks in `/proc/<pid>/cwd`

### uptime and tload
`uptime` - shows time since last reboot and other details about the system (users logged in, ect)
`w` - details about logged on users
`lscpu` - number of cpus and details

reminder: `ctrl + l` clear the screen

proc location for uptime
`cat /proc/uptime`
- second is showing the idle time for all cpus

`watch -n 4 uptime` - running the command every 4 seconds

`tload` - to constantly watch the load of the system.

### top and vmstat
`top -b -n1` - batch mode in 1 iteration
`top -b -n1 > file1` - output 1 iteration to a file

vmstat - collect process, memory, swap, etc...
check for `b` being a high number indicates many blocked processes

`vmstat -S m` - look at in mib
`vmstat -S K` - default in kb

check `cs` under cpu for context switchs per second. if we have alot of processes running it can get very high

## sysstat
install `yum install -r sysstat`
configuration: 
`cat /etc/cron.d/sysstat`
`cat /etc/sysconfig/sysstat`
`systemctl start sysstat`
`systemctl enable sysstat` - enable on startup
`systemctl status sysstat`

### additional sysstat tools
`iostat` - disk activity
`iostat -m` - in mb
`iostat -m 5 3` - run 3 times with 5 second gap

`pidstat -p <pid>` - process stats
`pidstat -p $$`

`mpstat -P ALL` - stats on all processes

## reporting with sar (system activity reporting)
`sar` - default is cpu utilization
`sar -u`- cpu
`sar -r` - report on memory utilization
`sar -b` - disk io 
`sar -n DEV` - network
`sar -q` - load average

seeing the log files for these activities
cd /var/log
sa dir - system activity files

`sar -s 14:50:00 -e 15:10:00` - specific start and end time for report
`sar -f /var/log/sa15` to switch log files

