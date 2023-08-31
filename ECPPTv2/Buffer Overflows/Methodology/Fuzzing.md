# Fuzzing
---
- We are going to *** Fuzz*** the application to find the approximate value of bytes at which the program crashes.

- Restart Immunity by using the Rewind button next to the red play arrow at the top. (Or Ctrl+F2)

- Then hit play. (or F9)

- We're going to use [[Fuzz.py]] to send our vulnerable command and additional data, increasing by 100 bytes (A's) with each attempt.
- This should have overwritten the EIP.

>💡 Make sure to note the EIP

