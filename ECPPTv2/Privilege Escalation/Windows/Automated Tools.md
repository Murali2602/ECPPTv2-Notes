# Automated Tools
---
## -   WinPEAS
    
 >[https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS/winPEASexe/binaries/x64/Release](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS/winPEASexe/binaries/x64/Release)
    
Just upload to the target system and let it run and analyze the infomartion later on
    
## -   Windows Exploit Suggester
    
> [https://github.com/AonCyberLabs/Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
    
In a windows shell type **_systeminfo_** and copy paste the stuff into a new **_sysinfo.txt_** in ur local machine to feed it to Windows-Exploit-Suggester
    
```bash
./windows-exploit-suggester.py --database <current_database> --systeminfo <sysinfo.txt>
```