# Host Discovery
---
Check out  [[Nmap]].

---
# IDLE Scan

##### Find a good zombie (Hping3)

In order to find a good zombie, we have to find a host with no active communications, in other words, we have to check if the host is sending packets to and from the network. This means that we have to find a host whose ID field does not change frequently.

To do this we can use hping3 sending packets to open ports at each host in the network, using the following command:

```bash
hping3 -S -r -p 135 10.50.97.10
```

where:

> -S tells Hping to send SYN flag

-r displays ID increments relatively

In this way, if the ID increments by 1 for each packet (id=+1), it means that the target is not sending packets through the network and is a good zombie candidate.

Another way to check if the target is a good candidate, is by using nmap. We can simply run the following command:

```bash
nmap -O -v -n 10.50.97.10
```

If the value of IP ID Sequence Generation is on Incremental, we can consider the target as a good candidate for our idle scan.

---
## IDLE Scan to check ports

Now that we have the address of a good zombie we can check if the target hosts have port 135 open:

Open a console, restart the Hping scan on the zombie (Task 9). This will show us ID's on the fly. Open another console and run the following command:

```bash
hping3 -a 10.50.97.10 -S -p 135 10.50.97.5
```

If the zombie ID increment is id=+2 on (Console 1) instead of id=+1 , we can deduce that port 135 on the target 10.50.97.5 is open . Otherwise, if the ID still increments by 1 , we can deduce that the port is closed .

Console 1:

![[Screenshot_20211212_181232.png]]

Console 2:

![[Screenshot_20211212_181207.png]]

The +2 increment from the hping3 scan on (console 1) while we run an hping idle scan in console2, shows an increment of +2 while scanning host 10.50.97.5 for port 135 from the spoofed source address of 10.50.97.10. This +2 sequence increment is indicative of port 135 being open on 10.50.97.5.