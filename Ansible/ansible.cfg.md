---
tags:
  - ansible
  - config
  - configuration
  - aumotation
---
```[defaults]
INVENTORY = inventory # defines the inventory file

[ssh_connections]
pipelining = true 
```

## Ansible_Pipelining 

Source: https://docs.ansible.com/ansible/latest/reference_appendices/config.html#ansible-pipelining
### Discription 

"*This is a global option, each connection plugin can override either by having more specific options or not supporting pipelining at all. Pipelining, if supported by the connection plugin, reduces the number of network operations required to execute a module on the remote server, by executing many Ansible modules without actual file transfer. It can result in a very significant performance improvement when enabled. However this conflicts with privilege escalation (become). For example, when using ‘sudo:’ operations you must first disable ‘requiretty’ in /etc/sudoers on all managed hosts, which is why it is disabled by default. This setting will be disabled if `ANSIBLE_KEEP_REMOTE_FILES` is enabled.*"
