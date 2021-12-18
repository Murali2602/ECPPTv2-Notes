# Badchars
---
- Reset Immunity (gotta do it every time).

- So, depending on the program you're attacking, certain hex characters might not have the effect you want them to have. For example, "\x00" is a null byte. With most programs, this marks the end of a string (Looking at you, C). So, if we have "\x00" in the middle of our shellcode, anything after that byte will not get copied into the stack (assuming we're taking advantage of something like strcpy()).

> ***Mona makes this process easier, as will Metasploit later.***

-  If your Windows machine doesn't have it already, copy the ***mona.py*** file into the PyCommands directory of Immunity Debugger (usually located at ***C:\Program Files\Immunity Inc\Immunity Debugger\PyCommands).***

- In Immunity Debugger, type the following to set a working directory for mona.

```bash
!mona config -set workingfolder c:\\mona\\%p
```

- Generate strings from [[Bytegen.py]] so you can copy it into [[Badchars.py]]

```bash
./bytegen.py
```

- Generate strings in mona

```bash
!mona bytearray -b '\\x00'
```

- Run [[Badchars.py]] and it will crash, overwrite the ***EIP***, and also throw all those hex symbols into memory and see how the program deals with them. Fortunately, you can have Mona do the hard part for you, seeing if there are any discrepancies.

```bash
!mona compare -f C:\\mona\\appname\\bytearray.bin -a <ESP>
```

- Mona will spit out a comparison. If she tells you sequential symbols, she might be lieing. If she gives 07 and 08, only include 07 in the next iteration.

- Repeat this process until Mona says that the results are unchanged. Now you have found all the bad characters.

- Save those bad characters, because we need them for shellcode.

