## Linux lab
install LAMP -> Apache Web Server, MySQL, PHP, phpmyadmin

## Basic command
    sudo apt update && sudo apt upgrade
    sudo apt-get update && sudo apt-get upgrade

## Firewall
    sudo ufw app list
    sudo ufw status

## Create a user account
    sudo adduser username

## Tools
    sudo apt install fish -y
    sudo apt install net-tools -y

shortcut

    sudo apt install fish -y && sudo apt install net-tools -y

## Installing GUI
    sudo apt install lightdm -y
    sudo apt install ubuntu-desktop -y
    sudo systemctl start lightdm.service
    sudo service lightdm start

## Installing ssh in Ubuntu
    sudo apt-get install openssh-client
    sudo systemctl enable ssh
    sudo ufw enable
    sudo ufw allow ssh
    sudo systemctl status ssh

shortcut

    sudo apt-get install openssh-client && sudo systemctl enable ssh && sudo ufw enable && sudo ufw allow ssh

## Installing Webmin
    sudo apt update && sudo apt upgrade
    sudo apt install software-properties-common apt-transport-https
    sudo wget -q http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] http://download.webmin.com/download/repository sarge contrib"
    sudo apt install webmin
    sudo systemctl status webmin
    dpkg -l | grep webmin
    sudo ufw allow 10000/tcp
    sudo ufw reload
    sudo ufw status

shortcut

    sudo apt update && sudo apt upgrade && sudo apt install software-properties-common apt-transport-https && sudo wget -q http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] http://download.webmin.com/download/repository sarge contrib" && sudo apt install webmin && sudo systemctl status webmin && dpkg -l | grep webmin && sudo ufw allow 10000/tcp && sudo ufw reload

Webmin set password

    sudo /usr/share/webmin/changepass.pl /etc/webmin root [new password]

https://[your server's IP]:10000/


refer : https://phoenixnap.com/kb/install-webmin-on-ubuntu

## Installing Apache Web Server
    sudo apt update && sudo apt upgrade
    sudo apt install apache2
    sudo ufw app list
    sudo ufw allow 'Apache'
    sudo ufw status
    sudo systemctl status apache2

shortcut

    sudo apt update && sudo apt upgrade && sudo apt install apache2 && sudo ufw allow 'Apache'

refer : https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04

## Installing MySQL
    sudo apt install mysql-server
    sudo mysql_secure_installation
    sudo systemctl status mysql
    sudo mysql

set the root password

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password123#@!';

Reload the grant tables in the MySQL database so that the changes can be applied without restarting the “mysql” service:

    FLUSH PRIVILEGES;

MySQL and change the root user’s authentication method back to the default, auth_socket. To authenticate as the root MySQL user using a password, run this command:

    mysql -u root -p
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
refer : https://linuxhint.com/install-mysql-on-ubuntu-22-04/, https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04

## Installing PHP
    sudo apt install php libapache2-mod-php php-mysql
    php -v

refer : https://nst-green.name/lamp-%E0%B8%9A%E0%B8%99-ubuntu-22-04-lts/

## Installing phpMyAdmin
    sudo apt update && sudo apt upgrade
    sudo mysql
    UNINSTALL COMPONENT "file://component_validate_password";
    exit
    sudo apt install phpmyadmin
    sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
    INSTALL COMPONENT "file://component_validate_password";
    sudo phpenmod mbstring
    sudo systemctl restart apache2

Configuring Password Access for the MySQL Root Account

    sudo mysql
    SELECT user,authentication_string,plugin,host FROM mysql.user;
    ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
    SELECT user,authentication_string,plugin,host FROM mysql.user;

Configuring Password Access for a Dedicated MySQL User

    sudo mysql
    CREATE USER 'sammy'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
    exit

You can now access the web interface by visiting your server’s domain name or public IP address followed by /phpmyadmin:

    https://localhost/phpmyadmin

refer : https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-22-04#configuring-password-access-for-a-dedicated-mysql-user
