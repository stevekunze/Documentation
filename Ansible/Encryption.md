---
tags:
  - ansible
  - aumotation
---
# create user with encrypted password
The easiest way to do this is with the `mkpasswd` command:
```bash
mkpasswd --method=sha-512
```
This will prompt for the plaintext password and will give a hashed password string. For password `secret`, get hash `$6$F4NWXRFtSdCi8$DsB5vvMJYusQhSbvGXrYDXL6Xj37MUuqFCd4dGXdKd6NyxT3lpdELN07/Kpo7EjjWnm9zusFg/LLFv6oc.ynu/`.
That would make the Yaml look like this:
```yaml
---
 - name: Create a login user
     user:
      name: fideloper
      password: '$6$F4NWXRFtSdCi8$DsB5vvMJYusQhSbvGXrYDXL6Xj37MUuqFCd4dGXdKd6NyxT3lpdELN07/Kpo7EjjWnm9zusFg/LLFv6oc.ynu/'
      groups: docker, sudo   # Empty by default.
      state: present
      shell: /bin/bash       # Defaults to /bin/bash
      system: no             # Defaults to no
      createhome: yes        # Defaults to yes
      home: /home/fideloper  # Defaults to /home/<username>
```

# Ansible Vault 
You can store a password that is necessary for a playbook in an encrypted file. 
1. create a yaml file and store the password in a variable. you can store multiple password in a file. Just call the variable inside the playbook to use a specific password
```yaml 
# this is the password file #filename is password.yaml
---
my_password: "supersecretpassword"
my_password2: "supersecretpassword2"
```
2. Encrypt the file by using asnible-vault. The File will be encrypted with AES256. You need to set a password to encrypt, decrypt, edit, view etc. 
`ansible-vault encrypt password.yaml`
3. call the variable inside the playbook to use the encrypted password (can also be an api key, cert etc.)
```yaml 
--- 

vars_file: 
	- password.yaml

- name: Create a login user
     user:
      name: fideloper
      password: " {{ my_password }}"
      groups: docker, sudo   # Empty by default.
      state: present
      shell: /bin/bash       # Defaults to /bin/bash
      system: no             # Defaults to no
      createhome: yes        # Defaults to yes
      home: /home/fideloper  # Defaults to /home/<username>
```
4. to run the playbook with the encrypted-vault-password you need to run: `ansible-playbook file.yaml --ask-vault-pass`

