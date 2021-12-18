# Finding Offset 
---
- Reset Immunity (Ctrl + F9)

- We really need to pinpoint*** EIP*** in order to control it, and control the service.

>**Metasploit Framework has a nifty couple tools for us `msf-pattern_create` .**

- It will give us a non-repeating pattern that we can send with our command. If we make it the right size, then we can copy whatever ends up in*** EIP*** after the crash and use `msf-pattern_offset`* to find the exact offset.*

- With that offset, we will own the EIP.

```bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l <bytes> 
```

- Double click the output to highlight, then ***Ctrl+Shift+C*** to copy it all.

- Paste it in [[Offset.py]] and run [[Offset.py]] copy the value from the*** EIP***.

- Then use the below tool to find out the exact offset match.
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l <bytes> -q <EIP>
```

- You can also check that offset with Mona.

