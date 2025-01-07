---
tags:
  - ansible
  - inventory
  - vars
  - aumotation
---
# Inventoryfile 

inventory file can be written in "yaml" or as "ini". I prefer the ini type. 

```
[hostgroup1]
192.168.178.100 # use IP 
exeample.local # use dns name if dns server is available

[hostgroup1:vars]
# define vars for specific group 
ansible_ssh_user=root # defines ssh user 
ansible_port=22 # defines the ssh port
ansible_ssh_private_key_file=~/.ssh/examplekey.pem # specifies the private key

```
