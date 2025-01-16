---
tags:
  - ansible
  - handlers
  - playbook
  - aumotation
---
**Source:** https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html
# Discription 

"*Sometimes you want a task to run only when a change is made on a machine. For example, you may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. Ansible uses handlers to address this use case. Handlers are tasks that only run when notified.*"

# Example 
```yaml 
---
- name: Test if Handler works
  hosts: all
  gather_facts: false
  become: true
  tasks:
    - name: Deny Password authentication
      ansible.builtin.lineinfile:
        path: "/etc/ssh/sshd_config"
        regexp: "^PasswordAuthentication"
        line: "PasswordAuthentication no"
        mode: '0644'
      notify:
        - Restart ssh

  handlers:
    - name: Retart ssh 
      ansible.builtin.service:
        name: 'sshd'
        state: restarted

```

## Flushing Handlers 

If you want to restart a service directly after a change you can call the *meta* Module
```yaml
- name: Make sure handlers are flushed 
  meta: flush_handlers 
```
