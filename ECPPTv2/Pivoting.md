# Pivoting

---
## Basics
Pivoting is the art of using access obtained over one machine to exploit another machine deeper in the network. It is one of the most essential aspects of network penetration testing, and is one of the three main teaching points for this room.

Put simply, by using one of the techniques described in the following tasks (or others!), it becomes possible for an attacker to gain initial access to a remote network, and use it to access other machines in the network that would not otherwise be accessible:

---
## Pivoting Types 
There are two main methods encompassed in this area of pentesting:

- Tunnelling/Proxying: Creating a proxy type connection through a compromised machine in order to route all desired traffic into the targeted network. This could potentially also be tunnelled inside another protocol (e.g. SSH tunnelling), which can be useful for evading a basic Intrusion Detection System (IDS) or firewall
 - Port Forwarding: Creating a connection between a local port and a single port on a target, via a compromised host
> **As a general rule, if you have multiple possible entry-points, try to use a Linux/Unix target where possible, as these tend to be easier to pivot from. An outward facing Linux webserver is absolutely ideal**.