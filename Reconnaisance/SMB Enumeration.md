# SMB Enumeration

### Use nmap and scan for ports 139,445 and gain as much information as you can.

```bash
nmap -A -p 139,445 10.130.40.70
```

---

## NMBLOOKUP

**Use NMBLOOKUP to enum NETBIOS table**

```bash
nmblookup -A 10.130.40.70
```
---
## NBTSCAN

**Use NBTSCAN to enum further**

```bash
nbtscan 10.130.40.70
```
---
## NBTSTAT NSE Script

This nmap script attempts to retrieve the target’s NetBIOS names and MAC address. By default, the script displays the name of the computer and the logged-in user; if the verbosity is turned up, it displays all names the system thinks it owns. It also shows the flags that we studied in nmblookup tool.

```bash
nmap --script nbstat.nse 192.168.1.17
```
---
## smb-os-discovery NSE Script

This NSE script attempts to determine the operating system, computer name, domain, workgroup, and current time over the SMB protocol (ports 445 or 139).

```bash
nmap --script smb-os-discovery 192.168.1.17
```
---
## SMBMap

SMBMap allows users to enumerate samba share drives across an entire domain. List share drives, drive permissions, share contents, upload/download functionality, file name auto-download pattern matching, and even execute remote commands.

```bash
smbmap -H 10.130.40.70
```
---
## smbclient

smbclient is samba client with an “ftp like” interface. It is a useful tool to test connectivity to a Windows share. It can be used to transfer files, or to look at share names.

```bash
smbclient -L 10.130.40.70
```

similarly to connect to a share

```bash
smbclient \\\\10.130.40.70\\ADMIN$
```
---
## smb-enum-shares NSE Script

Used to enum shares

```bash
nmap --script smb-enum-shares -p139,445 192.168.1.17
```
---
## Metasploit: smb_enumshares

```bash
msfconsole
use auxiliary/scanner/smb/smb_enumshares
```
---
## Null session

Check if is possible to list shared files and folders using null session.

---
## SMB Bruteforce

You can use Metasploit smb_login module or Nmap smb-brute script

---
## smb-vuln NSE Script

To check all SMB vulnerabilities available in the Nmap Scripting Engine we use the * with the script.

```bash
nmap --script smb-vuln* 192.168.1.16
```
---
## SMB Enumeration: Enum4Linux

enum4linux 10.130.40.70

---
# **[Source](https://www.hackingarticles.in/a-little-guide-to-smb-enumeration/)**

https://www.hackingarticles.in/a-little-guide-to-smb-enumeration/