## permissions

`ls -l`
`stat`

`stat -c %A` => symbolic permisions
`stat -c %a` => number permissions

0, ---  =   no permissions
1, --x   =   execute only
2, -w-  =   write only
3, -wx  =   write and execute (1+2)
4, r--  =   read only
5, r-x  =   read and execute (4+1)
6, rw-  =   read and write (4+2)
7, rwx  =   read and write and execute (4+2+1)

                    user    group   others

chmod 640 file1       rw-     r--     ---
chmod 754 file1       rwx     r-x     r--
chmod 664 file1       rw-     rw-     r--

### set permissions

`chmod 467 file1` 
`chmod u=r,g=rw,o=rwx file`

`chmod +x file1` => give everyone the execute permission on the file. 

`chmod -x file1` => remove execute for everyone.

the last value in the permissions is the `sticky bit` (not there if it is not set). it defines if you have permission to delete or not at the directory level
`drwxrwxrwt.` => lowercase t means it is set, uppercase T means it is not set

when set, only the owner of a file can delete files in the directory. 

`mkdir -m 1777 test` => create with stickybit set.

### chown
user and group owners

`id -u` => show userID
`id -un` => show username
`id -gn` => primary group name
`id -Gn` => secondary group names, when accessing files the secondary (complementry) groups are used to confirm permission

`wheel` group is the administrator group

`chgrp wheel file1` => set the primary group to wheel.

`newgrp wheel` => executes a new shell with the group as the primary

`chown root file2` => setting user owner to root
`chown root:root file2` => setting the user and group to root

`cp -a file2 /tmp/test.txt` => `-a` maintain attributes when copying file. 
