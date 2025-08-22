
# USER MANAGEMENT


| command | Description |
|--------|-------|
| adduser username | Add a user |
| useradd -G group username | Add a new user to group |
| useradd -G sudo username | Add a new user to  sudoer on ubuntu|
| useradd -G wheel username | Add a new user to  sudoer on Centos|
| sudo mkhomedir_helper username | Create home directory|
| passwd username | Setting password for new user |
| usermod -aG group username | Add existing user to group |
| userdel username | Delete user |
| userdel -r username | Delete user and home directory |
| du -shc /home/* | Check disk space for each user |
| cat /etc/group  | Check group of each user |
| usermod -s /bin/bash username | Change default bash for user |
