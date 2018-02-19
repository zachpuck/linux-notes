### RPM
`tree /var/cache/yum` -> yum cache

`rpm -qa`
`rpm -i <name.rpm>`
`rpm -e nmap`
`rpm -ql nmap` -> see what is included with a package
`rpm -qpl <name.rpm>`
`rpm -V nmap` -> verifying a pkg.

### yum
`yum install tree`
`yum install bash-completion`

`yum info bash-completion.noarch`

`yum version`

`yum remove nmap` -> remove pkg

`yum deplist nmap` -> shows dependencies

`yum list installed`
`yum list available`

### yum repositories
/etc/yum/repos.d

`yum info epel-release.noarch` -> enterprise linux

`less CentOS-Base.repo`

`yum repolist`
`yum reposlist all` -> shows disabled repos too

`mv C* /root/`

`vim local.repo`
```
[local]
name=Local Network Repo
baseurl=http://192.16.1.153
enabled=1
gpgcheck=0
```

`yum repolist` -> now see our local repo listed

### yum cache
`tree /var/cache/yum` -> tree view of all the yum cache

`yum makecache` -> checks repos and gets latest

`yum clean all` -> removes and downloaded pkgs cache data

### kernel updates
`uname -r`
`yum update kernel` -> installs the new kernel, it does not actually replace the older

`yum update` -> would show "update" for everything except for kernel it would show "install"

`vim yum.conf`
```
exclude=kernel*
```
excludes kernel from `yum update`

### managing services
enabling services after installing
`yum install httpd`
`nmap localhost` -> no web server listenting
`systemctl status httpd.service` -> state is disabled

`systemctl enable httpd.service`
`systemctl start httpd.service`

`nmap localhost` -> now shows listening on port 80

