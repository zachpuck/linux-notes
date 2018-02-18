# shared libraries

`ldd` - shows shared libraries for a specific executable

`ldd /usr/bin/ls`
`ldd /usr/bin/grep`

shared libraries have the `so` extention - shared objects

can also use `pmap $$`

### shared library locations
`/lib`
`/lib64`
 
 above are typically symlinks to `/usr/lib` and `/usr/lib64` dir

### to configure additional locations
`cd /etc/ld.so.conf.d`
`ls`
`mkdir /usr/local/lib/testing`
`cp /root/libdisplayuid.so !$`
`ls -l !$`
`chmod +x !$/libdisplayuid.so`
include in library cache via config files
`vim testing.conf`
- then point to the file location `/usr/local/lib/testing`

configure library path
LD_LIBRARY_PATH

### shared library cache
`ls -l /usr/local/lib/testing` -> pointing to the libdisplayuid.so
`cat showuid.c`

ldconfig -p | grep display

list out cache: 
`ls -l /etc/ld.so.cache`

`ldconfig` -> updates cache

ldconfig -p | grep display -> now shows after updating cache

`ldconfig -v` -> verbose updating of cache

