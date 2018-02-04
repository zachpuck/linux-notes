# Archiving Files

### tar

`tar -cvf /tmp/$USER.tar $HOME`
options
`c` => create
`v` => verbose
`f` => specify the file

`tar -tf test.tar`
options
`t` => look inside the file

`tar -xvf test.tar`
options
`x` => expand the tar into the current folder

### gzip & bzip2

`gzip test.tar` => compressing a tar file
`gunzip text.tar.gz` => unzip the tar file

`bzip2 test.tar` => even further compression
`bunzip2 test.tar.bz2` => unzip

`time tar -cvzf test.tar.gz $HOME` => time it takes to create the file, shows the difference in time to use gzip vs bzip2

options
`z` => compress with gzip
`j` => compress with bzip2

### cpio
used by RAM disk

`find -name '*.pdf' | cpio -o > /tmp/pdf.cpio` => copy input output to file

`cpio -id  < /tmp/pdf.cpio`
options
`i` => read in
`d` => create dir as needed

### dd - disk duplicator

`dd if=/dev/sr0 of=netinstall.iso` => input cdrom output iso

options:
`if` => input file
`of` => output file

option to wipe the data:
`fdisk -l` => listing my partions
`dd if=/dev/sda of=sda.mbr count=1 bs=512` => backup the first 512 bytes which is the master boot record

`dd if=/dev/zero of=/dev/sda count=1 bs=512` => this will wipe the master boot record

`dd if=sda.mbr of=/dev/sda` => restore the mbr
