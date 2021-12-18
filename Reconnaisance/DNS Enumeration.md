# DNS Enumeration
---
### Determine the DNS Server

DNS port is TCP/53 for zone transfer and, UDP/53 for DNS queries. All we need to do is to check if there is any host with the TCP port 53 opened.

```bash
nmap -sT -p53 172.16.5.1,5,6,10
```
---
### Determine the Domain Name

After discovering a couple of alive hosts and also the DNS Server address, our next step is to identify the network Domain Name. To do this, we can perform reverse lookup by using nslookup or dig.

```bash
nslookup 
>server 172.16.5.10 #The DNS server 
>172.16.5.5 #the server we want information on 

or

dig @172.16.5.10 -x 172.16.5.5 +nocookie #Here we can change the second address to the server we want informationn on and the first one is the actual dns server we found out 
```
---
### List additional hosts using DNS zone transfer

Zone Transfers are, usually, misconfigurations of a DNS server. They should be enabled, if required, only for trusted IP addresses (usually trusted downstream name servers).

When zone transfers are open to anyone, we can enumerate the whole DNS records for that zone. There are a couple of different tools that are able to do that, however, we will focus on dig.

The following command asks the DNS Server 172.16.5.10 to list all of its records (full zone transfer -t AXFR) for the domain named: sportsfoo.com . Note that we were able to discovery two new hosts: 10.10.10.6 and 10.10.10.10.

```bash
dig @172.16.5.10 sportsfoo.com -t AXFR +nocookie
```

The new hosts belong to a different network: 10.10.10.x.

> Note that we were not able to identify these hosts previously because, our ARP scan was performed within another network, 172.16.5.0/24. Furthermore, ARP broadcast requests can be send only in the same broadcast domain, thus they were unreachable.

>💡 Important: You'll notice in the previous "dig" commands we're using the "+nocookie" option with the command line. This is used to mitigate an error due to the way Microsoft DNS servers respond to the default "dig" options which send a DNS Cookie by default. Take note of this for future reference.

---
### DNS server name Brute Force(Forward Lookups)

One way that we can use to try to guess the DNS records of a DNS Server is to brute-force it. According to the provided hint, the hostnames of this environment matches with department's name. So, all we need to do is first create a .txt file with a list of department's names i.e.:

```bash
cat hostnames.txt
>marketing
>consulting
>sales
>support
>department1
>department2
>department3
>department4
>department5
```

With a list of possible departments, we can iterate using the following inline bash script. Where basically, we are performing a DNS Forward lookup using the host command for each line in the file:

```bash
for name in $(cat hostnames.txt); do host $name.sportsfoo.com 172.16.5.10 -W 2; done | grep 'has address'
```

> As we can see, we were able to discover 4 valid records. Clearly, with a largest dictionary file, we could discover more valid domain names.

> For example, with fierce, the DNS Brute Force tool, the list of possible hosts is 2280:

New code -

```bash
for name in $(cat /usr/share/fierce/hosts.txt); do host $name.sportsfoo.com 172.16.5.10 -W 2; done | grep 'has address'
```
---
### DNS REVERSE Lookups

The Reverse DNS lookups are DNS lookups where we use the IP address in order to obtain the hostname. You can use dig with the parameter -x in order to do such requests, however, we are going to use another shell script in order to try to obtain a more effective result.

First, let's create a file named iplist.txt file which will contain a list of IP addresses from 172.16.5.1 to 172.16.5.99. We can do that by running the following command:

```bash
root@kali:~/LABS/12# crunch 11 11 -t 172.16.5.%% -o iplist.txt
```

Now, type gedit ***reverse-dnnscript.sh*** in order to create a shell script which will use the file iplist.txt in order to perform reverse DNS lookups against every single IP on this list.

The shell script should have the following contents:

```bash
#!/bin/bash
for ip in $(cat iplist.txt); do dig @172.16.5.10 -x $ip +nocookie; done
```

Now run the script with the parameters | grep [sportsfoo.com](http://sportsfoo.com/) | grep PTR in order to filter and display only the records of our interest:

```bash
./reverse-dnsscript.sh | grep sportsfoo.com | grep PTR
```