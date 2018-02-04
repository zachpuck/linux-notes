### cat
wc = count number of word in a file
wc -l = count number of lines in a file
less = like cat but page through a file
!$ = used to reference last argument
inside less
/ = lets you search for something (ex /networking)
? = search backwards
use `n` to continue through the next matches

head = look at the top of the file (top 10 lines)
head -n 3 = top three lines

tail -n 3 /var/log/syslog = last 3 lines

yum list installed | grep ^kernel = lists items that begin with kernel (`^`)

ctrl a = move to the beginning of the line

### grep
grep server ntp.conf 

grep -E = enhanced regular expression

^ => begins with ex; `^server`
$ => ends with ex: `ver$`
^$ => emtpy lines

grep -E '[abc]{3}' /usr/share/dict/words = search the words file for any words that list abc in a row.

### sed - substitution operator

sed '/^#/d ; /^$/d' = using regex to search in a file for any word that starts with `#` and delete it or any line that is empty, the file is not modified though. 

sed -i => allows for in-place edit of the file. 

function clean_file {
    sed -i '/^#/d;/^$/d' $1
}

clean_file ncp.conf

### diff  - comparing files
echo new >> ntp.new = append the word new to the file

diff ntp.conf ntp.new = compare the two files

the results show results
5c5 = 5th line and 5th line are changes
11a12 = 11 line in first file does not have a 12th line that is added

1,3d0 = lines 1 through 3 have been deleted.

comparing binary: `md5sum`
md5sum /usr/bin/passwd = we can compare the checksum for binary files. 

rpm -V ntp => verify a executable against a database of what should be available

### find - searching 

find /usr/share/doc -name '*.pdf' = pdf files in the doc directory or any directory below it

-exec = execute ex: `find /usr/share/doc -name '*.pdf' -exec cp {} . \;` = copy every pdf it finds to the current directory

-iname = case insensitive
-delete = delete all the files it finds
-type l = symbolic links
-maxdepth 1 = just current directory
-size = search by size
-type f = regular files
-o = OR instead of default AND when using multiple options
find /boot -size +10000k -type f -exec du -h {} \;

