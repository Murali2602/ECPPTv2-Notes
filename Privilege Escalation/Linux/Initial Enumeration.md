# Initial Enumeration
---
# Important Sources -
> https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist

> https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_-_linux.html
---
## System Enumeration - 


| Command           | Information                                                   |
| ----------------- | ------------------------------------------------------------- |
| hostname          | used to display current system distro name                    |
| uname -a          | used to dispaly current user and kernel version of the system |
| cat /proc/version | similar to uname                                              |
| lscpu             | Check Architecture of the system                              |                  |                                                               |

---
## User Enumeration - 
| Command         | Information                                                  |
| --------------- | ------------------------------------------------------------ |
| whoami          | shows current user name                                      |
| id              | shows uid etc                                                |
| sudo -l         | shows the commands the user can run sudo as without password |
| cat /etc/passwd | we can see the users                                         |
| cat /etc/shadow | we can see the shadow file                                   |
| history         | Always check the history comeon ;)                                                             |

> cat/etc/passwd | cut -d : -f 1  
---
## Network Enumeration - 
| Command      | Information                                 |
| ------------ | ------------------------------------------- |
| ifconfig     | shows current network id                    |
| ip a         | same thing as above                         |
| route        | shows routing table                         |
| ip route     | same thing as above                         |
| arp -a       | shows the arp table                         |
| ip neigh     | same thing as above                         |
| netstat -ano | check the ports open and any other machines |              |                                             |


