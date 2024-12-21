# User  

## Root Passwort ändern und neuen User anlegen 

- run `passwd` as root to change root user password
- Create a user with a home direcoty and set bash as standard shell 
	- `useradd -g users -d /home/admin -m -s /bin/bash admin`
- change the password of the user with commadn `passwd admin`
- install user with command `apt install sudo`
- add the new user to the sudo group 
	`usermod -aG sudo admin`

