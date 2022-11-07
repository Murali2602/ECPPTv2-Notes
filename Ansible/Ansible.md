
## Master 

1.  Create an SSH key - `ssh-keygen -t ed25519 -C "ansible"` 
2. Copy this SSH key onto nodes  - `ssh-copy-id ~/.ssh/ansible <node-ip>`
3. Check the connection to nodes is working successfully - `ansible all -key-file ~/.ssh/ansible -i inventory -m ping` (Note - You should get a success or green colored output) 
4. Run `ssh-agent bash` & `ssh-add ~/.ssh/ansible`
5. Create an [[ansible.cfg]] file 


## Ad-hoc commands - 

**- Updating packages using `apt` **
-> `ansible all -m apt -a update_cache=true --become --ask-become-pass` 
> Here `all` is for all the hosts in the inventory, `-m` is the module used `-a` is the argument used, `update_cache` is basically updating packages,  `--become` is used to elevate privileges(sudo), `--ask-become-pass` is for asking the sudo password

**- Installing packages using `apt`**
-> `ansible all -m apt -a name=vim --become --ask-become-pass`
> This command will install the package vim onto all of the hosts (just replace name=vim with package you want)

**- Installing latest packages using `apt`**
-> `ansible all -m apt -a "name=vim state=latest" --becom --ask-become-pass`
> Here we give an extra option `state=latest` which installs the latest version of that package.


## Playbooks - 
Playbooks are written in YAML language.
- This is a very basic playbook example -> 
Example of a playbook(install-apache.yml) - 
```
---  
  
- hosts: all          #Applies to all of the hosts  
 become: true        #Used to elevate privileges  
 tasks:              #Define a set of tasks you want ansible to perform  
  
 -name: Update repository      #We will be using this syntax to update and install packages  
   apt:  
     update_cache: yes  
  
 - name: Install Apache2       #This is displayed in the output  
   apt:                        #This is the package manager name  
     name: apache2             #This is the package name  
     state: latest             #This is used to define the state of the package i.e. latest version of that package     
    
 - name: Install Vim  
   apt:  
     name: vim  
     state: latest           
 
 - name: Remove Vim  
   apt:  
     name: vim  
     state: absent             #Note: If we change "latest" --> "absent" it will remove the package
```

-> Running the playbook - `ansible-playbook --ask-become-pass install-apache.yml`


- **When condition with playbooks: ** 
-> We will be using the "when" condition to make sure that a task runs when it matches a condition such as when the package manager is debian.
Example: 
```
 - name: Install Vim  
   apt:  
     name: vim  
     state: latest       
     when: ansible_distribution == "Debian"       # If the OS is not Debian it will skip the task for that node

 - name: Install Apache2
   apt:
     name: apache2
     state: latest
     when: ansible_distribution in ["Debian", "Ubuntu"]     # This is used when you want to check for multiple thing(OS here).
``` 

## Improving Playbook - 

1. Consolidating -
	-> We will combine multiple packages installations into one - 
```
 - name: Install Packages  
   apt:                          
     name:    
       - apache2        # We join multiple packages into one task        
       - vim  
     state: latest  
   when: ansible_distribution == "Debian"
``` 

2. Targeting Specific Nodes -
-> We can make ansible run stuff on particular nodes by specifying them in the inventory and the playbook - 
Example of inventory file - 
```
[Debian]  
10.10.30.12  
10.10.30.13  
  
[CentOS]  
10.10.30.14
```
Example of a task that only runs on Debian hosts - 
```
---  

# This will run on all the hosts
- hosts: all             
 become: true           
 tasks:                 
  
  
   ##Debian     
 - name: Update repository         
   apt:  
     update_cache: yes  
   when: ansible_distribution == "Debian"  
  
   ##CentOS  
 - name: Update repository  
   yum:  
     update_cache: yes  
   when: ansible_distribution == "CentOS"  


# This will run only on Debian hosts (Specified in inventory)
- hosts: Debian  
 become: true  
 tasks:  
  
 - name: Install Packages  
   apt:                          
     name:    
       - apache2                
       - vim  
     state: latest  
   when: ansible_distribution == "Debian"  
  
# This will run only on CentOS hosts (Specified in inventory)
- hosts: CentOS  
 become: true  
 tasks:    
  
 - name: Install Packages  
   yum:  
     name:    
       - httpd  
       - php  
     state: latest  
   when: ansible_distribution == "CentOS"
```


## Managing Files - 

1. Basic File Management - 
-> 
```
- name: copy file  
 copy:               
   src: lol.txt     
   dest: /home/murali/lol.txt  
   owner: root  
   group: root  
   mode: 0644
```