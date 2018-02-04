### touch
can be used to create files and modify timestamp on existing files

touch -d => lets you define the access and modify time of a file.

stat -> shows all the details of a item

!s => run the last command that started with s

### vim
`vimtutor` => lessons on using `vim`
:help

:set showmode (if the mode ex: `INSERT` is not showing)

:set invnumber

~/.vimrc => settings override file
```
set showmod nohlsearch nonumber
set ai ts=4 expandtab
abbr _sh #!/bin/bash
nmap <C-N> :set invnumber<CR>
```

O (uppercase) => insert above above the current line
o (lowercase) => below the current line

1 + G => top of file
G => bottom of file
2 + G => takes you to line 2

i => insert before cursor position
a => appends
I => inserts at start of line
A => appends to end of line 

k => move up one line
yy => copy the line
p => paste below the line
P (uppercase) => paste above the line

2yy => will copy the next two lines

dw => delete one word
d$ => delete to the end of the line
dd => delete the entire line
2dd => delete two lines
dG => deletes to the end of the file
u => undoes the last change

^ => move to the beginning of the line
g~~ => change the entire lines to the opposite case
gUU => toggles the whole line to uppercase
~ => toggle one character at a time to the opposite case 

:e! => revert to the last saved file
