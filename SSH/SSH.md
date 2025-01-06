---
tags:
  - ssh
  - strato
  - key
  - privatepublickey
---
# Creating A Keypair 

```ad-important
Private-Key file permission is always 600. Only Read/Write permissions for the User, which is using the key for authentication. Key should be protected with a passphrase.
```


3. Create SSH Keypair with ed25519
```bash
ssh-keygen -t ed25519 -f ~/.ssh/host_ed25519
```
2. Copy the public key to the remote server  
```bash
ssh-copy-id -i ~/.ssh/keyfilename user@ip
```
# Hardening the server
1. Edit sshd_config 
```shell 
nano /etc/ssh/sshd_config
```
2. do not allow empty password 
```plaintext
PermitEmptyPasswords no
```
3. do not allow ssh login with root user 
```
PermitRootLogin no
```
4. Change standard ssh port, exp. 2222 or 27 
```plaintext
#Run SSH on a non-standard port
#Port 22
Port 27
```
5. deny login with password and allow publickey authentication  
```plaintext
PasswordAuthentication no
PublicKeyAuthentication yes
```
6. SSH Service neu-starten 
```shell
systemctl restart sshd
```
## Misc 
### Login with a specific key 
*-i* option to specify the desired key. *-p* the port. Username@Destination.
```bash
ssh -i strato-steve_key -p 2007 steve@85.214.88.98
```
### Deny/allow specific users 
```plaintext
DenyUsers root 
AllowUsers admin
```
### Testing the keypair 
- Displays the public key that belongs to the private key
```bash
ssh-keygen -y -e -f username_key
```
- print the public key 
```bash
cat username_key.pub
```
### SSH Service restart
- SSH-Dienste neu-starten 
```bash 
systemctl restart sshd.service systemctl restart ssh.service
```


