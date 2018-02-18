# Processes

### Using ps
ps options
`man ps`
versions of ps accept several kinds of options

unix style with all process
`ps -e`

BSD style of all process
`ps aux`

mixing styles unix/gnu
`ps -e --forest`
- shows a process tree style
alternatively just use `pstree` (to install if missing `yum install psmisc`)

full listing
`ps -f` or extra full `ps -F`

long listing
`ps -l`
`ps -ly` shows memory used

all process
`ps aux`
`ps -elf`

find specific listing
`ps -elf | grep sshd`

### /proc Dir and $$ Variable
`ls /proc` - running process on system

`echo $$` - lists process ID of current running process

`cd $$` - move into the currently running process /proc directory

`ls -l cwd` - list out details of current working directory
`ls -l exe` - show the current executable we are using in this directory (while inside of `/proc/<pid>` dir)

find the loadavg - helps see the number of processes running
`cat loadavg` or `cat /proc/loadavg`

### kill cmd
`stty -a` - list keyboard shortcuts

`kill -l` - all the signals

to kill a pid
`kill <pid>`

to kill a pid forcefully
`kill -sigkill <pid>`

shortcut cmds (pgrep and pkill)
`pgrep sshd`

`ps -F -p $(pgrep sshd)`

`pkill sleep`  kill all sleep processes


### top
`top` - review all load,process, memory,cpu of the system
managing top:
change sort `f`
select new type to sort by `s`
back to new sort `esc`
quite `q`

## process priority
### backgrounding tasks
`bg` and `fg`

start process in background
`sleep 1000&`

list process running in background
`jobs`

move process to background:
`sleep 1000`
hit `ctrl +z` stopped the job and get your termanial back
`jobs` shows it as "stopped"
type `bg` to move the job to a background process
`fg` to move the job back to the forground

bring a different job to foreground
find the number under `jobs`
`fg 1`

list details of one process
`ps -p <pid>`

### working with pri and ni
default nice value of 0
`nice -n 19 sleep 1000` - sets it to the lowest priority

higher the `pri` number the lower the priority

changing the priority of the process
`renice -n 10 -p <pid>` - only root can increase priority, users can decrease priority only

changing defaults

`vim /etc/security/limits.conf`
controls the nice value 

