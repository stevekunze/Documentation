# User  

## New User + Sudo 

- run `passwd` as root to change root user password
- Create a user with a home direcoty and set bash as standard shell 
	- `useradd -g users -d /home/admind -m -s /bin/bash admind`
- change the password of the user with command `passwd admind`
- install user with command `apt install sudo`
- add the new user to the sudo group 
	`usermod -aG sudo admind`

### Passwordless sudo (optional)


1. Edit sudoers file: `sudo nano /etc/sudoers`
2. Find a line which contains **includedir /etc/sudoers.d**
3. Below that line add: **username ALL=(ALL) NOPASSWD: ALL** , where username is name of the user (for me admind on most servers)
