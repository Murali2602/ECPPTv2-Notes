# Initial Enumeration
---
## Important Sources -
> https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation

>https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html

---
### -   **System Enumeration**
    
- System Info -        
```bash
systeminfo 
        
or 
        
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"
```
        
- WMIC - 
```bash 
wmic logicaldisk get caption
```
---
### -   **USER Enumeration**
```bash
whoami
whoami /priv
whoami /groups
net user
net localgroup administrator 
```
---
### -   **Network Enumeration**
```bash
ipconfig /all
arp -a
route print 
netstat -ano
```
---
### -   **Password Hunting**
```powershell
findstr /si password *.txt 
findstr /si password *.xml
findstr /si password *.init 
```
---
### -   **AV Enumeration**
```PowerShell
sc query windefend
netsh advfirewall firewall dump
netsh firewall show state
netsh firewall show config
```
---