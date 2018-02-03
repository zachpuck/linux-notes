tty = teletypewriter = any terminal on linux/unix systems.
who = who is logged on
type ls = shows the options being run with the command

##ls 
-a = all
-F = all files
light blue = symbolic links with @ symbol when using -F
green = executable (* = executable when using -F)
-r = reverse sort
-t = time field
-h = human readable format
-d = list the current directory only

file types:
left most character when using ls -l
ex: drwxr-xr-x  4 root root   4096 Jan  7 16:58 systemd
d = directory
c = character input
b = block device
l = symbolic link
- = regular file
ls -l $(tty)

lsb = available block devices (disk and partitions)

ls -l /dev/sda*
* = wildcard char
? = single char
[12] = sda1 or sda2

ls -l /etc/system-release (shows a symlink and where it is pointing to)

lsb_release -d = list the description for the release (binary file that was installed)

rpm -qf /usr/bin/lsb_release = query database where file is installed from

shortcut = rpm -qf $(which lsb_release)

##cp, cat, mv, rm

/etc/passwd = password/user file for the machine

-i = interactive mode, asks if you want to override a file that exists

mv = rename and/or move to another directory

rm -i * = remove files but prompt before 

rm *hosts = remove all files that end with `hosts` (* means zero or more characters matching)

## Directorys
mkdir:
-p = creates parent directory as well
-m = set permissions 

!rm = rmdir = remove a directory
rm -rf = removes directory and content

mkdir one two
touch one/file{1..5} = create 1-5 files

cp -R one two = copy recursively everything in dir one to dir two

tree (need to isntall) = shows directory listing of files like an outline

mkdir -m 777 d1 = mkdir with all permissions user and group
mkdir -m 700 d2 = mkdir with read/write for user

## Links

Hard Links:
ls -ld /etc
drwxr-xr-x. 110 root root 8912 Dec 15 18:15 /etc
the `110` represents the hard link count, 110 names linked to the same metadata
ls -ldi /etc
ls -ldi /etc/. - this represents the current directory. 

this helps identify how many subdirectorys a directory has. (it always has 2 for . and ..)

linking files:
echo hello > f1
ln f1 f2 = link file 1 to file 2
ln -s f1 f2 = symbolic link file 1 to file 2 (symoblic lets you cross file system boundries)

ls -l => listing files (metadata as well)
ls -i => inode entry 
ls -lh => human readable
-a => hidden files
-ltr = long listing time stamp reversed order
ls -F => supports color

regular files => - 
Directory => d
symoblic links => l
block dives => d
chracter devies(tty) => c
named pipes => p
sockets => s

