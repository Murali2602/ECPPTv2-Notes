
#### Allow ssh root access and restart ssh - 

`sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && systemctl restart ssh`

