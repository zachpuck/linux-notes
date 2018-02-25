`df -hT` -> 'T' shows the type of file system

#### quota on ext4 systems

`quota` (hit tab) -> list all the quota commands avialable

`vim /etc/fstab` ->  add in `usrquota` on /dev/sdb6

`quotacheck -mau` -> make a user quota database

`quotaon /dev/sdb6` -> enable the quota

`repquota -uv /dev/sdb6` -> report on users in verbose mode

`setquota -u bob 20000 25000 0 0 /dev/sdb6` -> soft limit then hard limit, no quota on group so (0, 0)

`edquota -u bob` -> edit quota file for bob on all file systems that bob has quotas on

#### xfs quota management
uquota user), gquota (group), pquota (project)

`xfs_quota`
    `df -h`
    `quota bob`
`xfs_quota -c 'quota -h bob'`

