# Scan Techniques
---

| Switch | Example              | Description       |
| ------ | -------------------- | ----------------- |
| -sS    | nmap 192.168.1.1 -sS | ***TCP SYN*** port scan |
| -sU    | nmap 192.168.1.1 -sT | ***UDP*** Port scan     |

---
# Host Discovery
| Switch | Example                 | Description                                |   
| ------ | ----------------------- | ------------------------------------------ | 
| -sn    | nmap 192.168.1.1/24 -sn | Disable Port Scanning. Only host discovery |     
| -Pn    | nmap 192.168.1.1-5 -Pn  | Disable Host Discovery. Only port scanning |    
| -n     | nmap 192.168.1.1-5 -n   | Never Do ***DNS Resolution***              |   
| -PE    | nmap 192.168.1.1-5 -PE  | Enables ***ICMP echo*** request(ping scan) |    
| -PR    | nmap 192.168.1.1-5 -PR  | Arp Discovery on Local host                |    
> ***Note:*** If you only use -sn without -PE, nmap uses ICMP requests, but will also send a TCP SYN packet on ports 80 and 443 of each host.
---
# Service and Version Detection
| Switch | Example              | Description                                                               |
| ------ | -------------------- | ------------------------------------------------------------------------- |
| -SV    | nmap 192.168.1.1 -sV | Attempts to detect the version of the service running on the port.        |
| -A     | nmap 192.168.1.1 -A  | Enables OS detection, version detection, script scanning, and traceroute. |       |                      |                                                                           |

---
# OS Detection
| Switch | Example             | Description                                            |
| ------ | ------------------- | ------------------------------------------------------ |
| -O     | nmap 192.168.1.1 -O | Remote OS detection using TCP/IP stack fingerprinting. |                     |                                                        |     |     |     |

---
# NSE Scripts
| Switch   | Example                            | Description                                                                   |
| -------- | ---------------------------------- | ----------------------------------------------------------------------------- |
| -sC      | nmap 192.168.1.1 -sC               | Scan with*** default NSE scripts***. Considered useful for discovery and safe |
| --script | nmap 192.168.1.1 --script=banner   | Scan with a ***Single Script.***(Replace 'Banner')                            |
| --script | nmap 192.168.1.1 --script=smb*     | Scan with a ***Wildcard***                                                    |
| --script | nmap 192.168.1.1 --script=smb,http | Scan with ***2 Scripts***                                                     |          |                                    |                                                                               |          |                                    |                                                                               |

---
# Other Useful Nmap Commands
| Command                                                        | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- |
| nmap 192.168.1.1-1/24 -PR -sn -vv                              | Arp discovery only on local network, no port scan              |
| nmap -Pn --script=dns-brute domain.com                         | Brute forces DNS hostnames guessing subdomains                 |
| nmap -p80 --script http-unsafe-output-escaping scanme.nmap.org | nmap -p80 --script http-unsafe-output-escaping scanme.nmap.org |
| nmap -p80 --script http-sql-injection scanme.nmap.org          | Check for SQL injections                                                               |

