### STDOUT
`1>` => explicitly says STDOUT to overwrite the file. the one is typically left off and it is assumed it is STDOUT.

`>` => overwrite a file 
`>>` => appending to a file

### noclobber
prevent overritting a file

set -o => list out shell options
set -o noclobber => turn the option on
set +o noclobber => turns the option off

`>|` => overwritting the noclobber option

`date +%F >| file1` => will overwrite even with noclobber on

`Ctrl + r` => reverse search history

### STDERR
`2>` => sends STDERR to a file, `ls /etcw 2> err.txt`

`2> /dev/null` => special device file to throwaway the output.

`&>` => sends STDOUT and STDERR to a file

### STDIN
`df -hlT` => the `T` shows the type
`<` => read into standard input

### Here Documents
creating small files at the command line

`cat > newfile <<END` => reading into the file until we hit the end. this gives a continuation prompt.
`END` => to end the continuation prompt.

### Command Pipelines
`|` => unnamed pipes

`cut -f7 -d: /etc/passwd` => list field 7 with : as the delemeter.

`cut -f7 -d: /etc/passwd | sort | uniq |wc -l` => passing multiple commands on to the next command

### Named Pipes
interprocess communication

`mkfifo mypipe` => creating a pipefile

`ls -l` => the `p` at the beginning indicates it is a pipe file.

if you send someting to a pipefile (`cat testfile > mypipe`) you can consume it from anoter process by using the pipefile as input (`wc -l < mypipe`)

### tee
allows you to send out to 2 channels
STDOUT and to a file
`ls -l /etc | tee newfile`