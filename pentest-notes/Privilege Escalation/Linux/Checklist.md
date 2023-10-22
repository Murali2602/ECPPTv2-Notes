
## Automated Enumeration Tools 
LinPeas: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS

## Kernel Exploits
Dirty Cow and stuff

## Sudo 
Sudo -l and LD_PRELOAD
https://gtfobins.github.io

## SUID 
`find / -type f -perm -04000 -ls 2>/dev/null` will list files that have SUID or SGID bits set.

## Capabilities
`getcap -r / 2>/dev/null`

## Cron Jobs
Check `/etc/crontab`

## Path
`echo $PATH`
`export PATH=/tmp:$PATH`

## NFS
Check for `no_root_squash`
`cat /etc/exports`
`showmount -e <victim ip>` 

