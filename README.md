## Ubuntu Linux install LAMP or LEMP
Ubuntu install LAMP -> Apache Web Server, MySQL, PHP, phpmyadmin
Ubuntu install LEMP -> Nginx, MySQL, PHP, phpmyadmin

- [Ubuntu Linux install LAMP or LEMP](#ubuntu-linux-install-lamp-or-lemp)
- [Basic command](#basic-command)
- [Firewall with UFW](#firewall-with-ufw)
  - [Enabling UFW](#enabling-ufw)
  - [Allowing UFW](#allowing-ufw)
  - [Denying Connections](#denying-connections)
  - [Status of UFW](#status-of-ufw)
- [Create a user account](#create-a-user-account)
- [Tools](#tools)
- [Installing ssh in Ubuntu](#installing-ssh-in-ubuntu)
- [Installing GUI](#installing-gui)
- [Installing Webmin](#installing-webmin)
- [Installing Apache Web Server](#installing-apache-web-server)
  - [Installing Apache Web Server for PHP8.2](#installing-apache-web-server-for-php82)
- [Installing Nginx](#installing-nginx)
  - [Fix Permission](#fix-permission)
- [Installing MySQL](#installing-mysql)
- [Installing PHP](#installing-php)
  - [CAVEATS:](#caveats)
  - [PHP 8.1](#php-81)
  - [PHP 8.2](#php-82)
  - [PHP 8.3](#php-83)
  - [Config Nginx](#config-nginx)
  - [Test PHP](#test-php)
- [Installing phpMyAdmin](#installing-phpmyadmin)
  - [phpMyAdmin for Nginx](#phpmyadmin-for-nginx)
- [MySQL Workbench Installation](#mysql-workbench-installation)

## Basic command
    sudo apt update && sudo apt upgrade
    sudo apt-get update && sudo apt-get upgrade

## Firewall with UFW

### Enabling UFW
    sudo ufw enable

### Allowing UFW
    sudo ufw allow ssh

or port

    sudo ufw allow 22

### Denying Connections
    sudo ufw deny http

or use number : ```sudo ufw status numbered```

    sudo ufw delete 2

or Actual Rule

    sudo ufw delete allow http
    sudo ufw delete allow 80

### Status of UFW
    sudo ufw status numbered
    sudo ufw app list
    sudo ufw status
    sudo ufw status verbose

refer : https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04#step-3-allowing-ssh-connections

## Create a user account
    sudo adduser username

## Tools
    sudo apt install fish -y
    sudo apt install net-tools -y

shortcut

    sudo apt install fish -y && sudo apt install net-tools -y

## Installing ssh in Ubuntu
    sudo apt-get install openssh-client
    sudo systemctl enable ssh
    sudo ufw enable
    sudo ufw allow ssh
    sudo systemctl status ssh

shortcut

    sudo apt-get install openssh-client && sudo systemctl enable ssh && sudo ufw enable && sudo ufw allow ssh

## Installing GUI
    sudo apt install lightdm -y
    sudo apt install ubuntu-desktop -y
    sudo systemctl start lightdm.service
    sudo service lightdm start

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

https://localhost:10000/


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

### Installing Apache Web Server for PHP8.2
    sudo add-apt-repository ppa:ondrej/apache2
    sudo apt-get update
    sudo apt-get install apache2
    sudo ufw app list
    sudo ufw allow 'Apache'
    sudo ufw status
    sudo systemctl status apache2
    apache2 -v

## Installing Nginx
    sudo apt update
    sudo apt install nginx
    sudo ufw allow 'Nginx HTTP'
    sudo ufw status

Checking your Web Server

    systemctl status nginx

### Fix Permission
    cd /var/www/html
    ls -l
    sudo chown -R admin:admin /var/www/html

test

    nano index.html
```bash
<!DOCTYPE html><html><body><h1>My First Heading</h1><p>My first paragraph.</p></body></html>
```

refer nginx: https://karnyong.medium.com/%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-lemp-stack-%E0%B8%9A%E0%B8%99-ubuntu-22-04-vm-%E0%B9%81%E0%B8%96%E0%B8%A1%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-phpmyadmin-d589599f891a

refer nginx : https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-22-04

refer : https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04

## Installing MySQL
    sudo apt install mysql-server
    sudo mysql_secure_installation
    sudo systemctl start mysql.service
    sudo systemctl status mysql
    sudo mysql

set the root password
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password123#@!';
```

Reload the grant tables in the MySQL database so that the changes can be applied without restarting the “mysql” service:
```bash
FLUSH PRIVILEGES;
```

Run the security script with sudo:

    sudo mysql_secure_installation

MySQL and change the root user’s authentication method back to the default, auth_socket. To authenticate as the root MySQL user using a password, run this command:

    sudo mysql -u root -p

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```

refer : https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04, https://linuxhint.com/install-mysql-on-ubuntu-22-04/, https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-22-04

## Installing PHP

### CAVEATS:
1. If you are using php-gearman, you need to add ppa:ondrej/pkg-gearman
2. If you are using apache2, you are advised to add ppa:ondrej/apache2
3. If you are using nginx, you are advised to add ppa:ondrej/nginx-mainline
   or ppa:ondrej/nginx

### PHP 8.1
    sudo apt install php libapache2-mod-php php-mysql
    php -v

refer : https://nst-green.name/lamp-%E0%B8%9A%E0%B8%99-ubuntu-22-04-lts/

### PHP 8.2
    sudo apt update && apt upgrade -y
    sudo add-apt-repository ppa:ondrej/php
    sudo apt-get update
    sudo apt install php8.2 -y
    php --version

refer : https://techvblogs.com/blog/install-php-8-2-ubuntu-22-04

### PHP 8.3
    sudo apt update && sudo apt upgrade -y
    sudo apt-get install ca-certificates apt-transport-https software-properties-common
    sudo add-apt-repository ppa:ondrej/php
    sudo apt-get update
    sudo apt-get install php8.3
    sudo php8.3 --version

refer : https://www.linuxtuto.com/how-to-install-php-8-3-on-ubuntu-22-04/

### Config Nginx
    sudo nano /etc/nginx/sites-enabled/default
    add index.php and change php7.4-fpm -> php8.2-fpm
    sudo nginx -t
    sudo service nginx restart

### Test PHP
    sudo nano /var/www/html/info.php
    <?php phpinfo(); ?>

http://localhost/info.php

## Installing phpMyAdmin
    sudo apt update && sudo apt upgrade
    sudo mysql

```bash
UNINSTALL COMPONENT "file://component_validate_password";
```

```bash
exit
```

    sudo apt install phpmyadmin
    sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

```bash
INSTALL COMPONENT "file://component_validate_password";
```

    sudo phpenmod mbstring
    sudo systemctl restart apache2

Configuring Password Access for the MySQL Root Account

    sudo mysql

```bash
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
```

```bash
SELECT user,authentication_string,plugin,host FROM mysql.user;
```

Configuring Password Access for a Dedicated MySQL User

    sudo mysql

```bash
CREATE USER 'sammy'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
```

```bash
GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
```

```bash
    exit
```

### phpMyAdmin for Nginx
    sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

You can now access the web interface by visiting your server’s domain name or public IP address followed by /phpmyadmin:

http://localhost/phpmyadmin

refer : https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-22-04#configuring-password-access-for-a-dedicated-mysql-user

refer nginx: https://karnyong.medium.com/%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-lemp-stack-%E0%B8%9A%E0%B8%99-ubuntu-22-04-vm-%E0%B9%81%E0%B8%96%E0%B8%A1%E0%B8%95%E0%B8%B4%E0%B8%94%E0%B8%95%E0%B8%B1%E0%B9%89%E0%B8%87-phpmyadmin-d589599f891a

## MySQL Workbench Installation
    sudo apt update
    sudo snap install mysql-workbench-community

refer : https://www.geeksforgeeks.org/how-to-install-mysql-workbench-on-ubuntu/
