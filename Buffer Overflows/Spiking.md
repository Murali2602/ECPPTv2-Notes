# Spiking
    
 - We're going to use Spike to test which commands are vulnerable to buffer overflows.
    
>💡 Spike is accessed with `$ generic_send_tcp`
       
## Usage:
    
```bash
    generic_send_tcp host port spike_script SKIPVAR SKIPSTR 
    #Example
    ./generic_send_tcp 192.168.1.100 701 something.spk 0 0
```

#### Spike.Spk -
 ```bash
    s_readline(); #to read the banner
    s_string("OVERFLOW1 "); #our command to test, don't forget the space afterwards
    s_string_variable("0"); #any additional strings to add each time
  ```
    
- This is going to make a ton of connections, passing the string with fuzzed information.
    
- Immunity should crash, if the command is vulnerable.
    
- Look at your register values. See if it was able to overwrite the ***EIP***.

#bufferoverflow