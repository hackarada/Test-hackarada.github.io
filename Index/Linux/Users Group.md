# Users/Group

---

## User Management

### list all users

    less /etc/passwd 

or 

     cat  /etc/passwd

### Adding User

    Sudo useraddd -[options] [userName]

### set password for user

    passwd <username>

### add user to Sudoers

    usermod -aG sudo username 

or 

    apt-get install adduser

Delete user

    user del

[https://linuxize.com/post/how-to-list-users-in-linux/](https://linuxize.com/post/how-to-list-users-in-linux/)