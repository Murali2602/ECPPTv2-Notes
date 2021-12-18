# Jump Point
---
- We have the EIP, but what do we do with it?

- It needs an address. It needs an address that will jump to a new stack frame.

- We need a `jmp esp` .

- Fortunately, that's easy in Immunity with Mona.
  
```bash
!mona jmp -r esp -cpb "\\x00\\x0a\\x0d"
```

- This will return you a list of memory addresses that you can use. Pick one and save it. We'll need it in a second.

- Oh, you'll have to turn it into little endian with my code. The 32 bit address*** \xAABBCCDD*** looks like this in 4 bytes ***\xDD\xCC\xBB\xAA***.

