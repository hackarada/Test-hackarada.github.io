# MySQL

---

[https://bit.ly/37R7HiZ](https://bit.ly/37R7HiZ)

Install MySQL - UBUNTU

Install the MySQL server by using the Ubuntu operating system package manager:

    sudo apt-get update
    sudo apt-get install mysql-server

The installer installs MySQL and all dependencies.

If the secure installation utility does not launch automatically after the installation completes, enter the following command:

    sudo mysql_secure_installation utility

This utility prompts you to define the mysql root password and other security-related options, including removing remote access to the root user and setting the root password.

# **Allow remote access**

If you have iptables enabled and want to connect to the MySQL database from another machine, you must open a port in your server’s firewall (the default port is 3306). You don’t need to do this if the application that uses MySQL is running on the same server.

Run the following command to allow remote access to the mysql server:

    sudo ufw enable
    sudo ufw allow mysql

Start the MySQL service

    sudo systemctl start mysql

### Mysql Shell

    /usr/bin/mysql -u root -p

start mysql service

    sudo systemctl start mysql

start at starup

    sudo systemctl enable mysql

view users

    SELECT User, Host, authentication_string FROM mysql.user;