## *2025-09-27* — Sudo, Users & Permissions

**What I practiced:**   
- Using sudo and root to run admin commands
- Creating a new user and setting a password
- Setting file permissions (read/write/execute) for users, groups, and others
- Changing owner of files and directories
 
**Why it matters:**  
File permissions keep a system safe and organized. Without them, anyone could edit system files or someone else’s work, which makes it easy to break things by accident.

**Commands (*cheatsheet*):**  
- `sudo <command>` | run a command with admin rights
- `sudo su` | switch to root user
- `whoami` | check which user you’re logged in as
- `sudo tail /var/log/auth.log` | view recent sudo commands from system logs
- `sudo adduser <username>` | create a new user
- `passwd <username>` | set or change a password
- `su - <username>` | switch to another user
- `sudo usermod -aG sudo <username>` | give a user sudo (admin) rights
- `sudo deluser <username> sudo` | remove sudo rights
- `cat /etc/group` | see all groups on the system
- `sudo groupadd <groupname>` | create a new group
- `groups <username>` | see what groups a user belongs to
- `sudo gpasswd -d <username> <groupname>` | remove user from a group
- `sudo groupdel <groupname>` | delete a group
- `ls -l` | see file permissions (r=read, w=write, x=execute)
- `chmod <octal> <file>` | change file permissions
- `sudo chown <user> <file>` | change file owner
- `sudo chgrp <group> <file>` | change file group
- `sudo chown -R <user>:<group> <directory>` | recursively change ownership

**Key outcome:**  
I learned how to control access in Linux by managing users, groups, and file permissions.

**Next step:**   
Finish last part of linux fundamentals (standard streams, environment variables and aliases).
