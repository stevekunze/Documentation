# User  

## New User + Sudo 

- run `passwd` as root to change root user password
- Create a user with a home direcoty and set bash as standard shell 
	- `useradd -g users -d /home/admind -m -s /bin/bash admind`
- change the password of the user with commadn `passwd admind`
- install user with command `apt install sudo`
- add the new user to the sudo group 
	`usermod -aG sudo admind`

## Change SSH Configuration 

