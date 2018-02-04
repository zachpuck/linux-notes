### script
`man script`

`script` => default is to record the inputs into the 'typescript' file. 

`mkfifo /tmp/mypipe` => create a named pipe file

`script -f /tmp/mypipe` => start a script session sending all the inputs to the named pipe. 

in seperate terminal type `cat /tmp/mypipe` will output all the things typed in.

### screen
run same command across multiple systems.

runtime config file `vim ~/.screenrc`

screen -t master 0 bash
screen -t s1 1 ssh server1
screen -t s2 2 ssh server2

to navigate between the screens
ctrl + a n => next
ctrl + a p => previous
ctrl + a " => list screens

`ctrl + a : "#" stuff "yum install -y zsh^M"` => command to pass to all screens