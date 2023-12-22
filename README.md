# Linux
Linux lab
## Basic comman:
    sudo apt update && sudo apt upgrade
or

    sudo apt-get update && sudo apt-get upgrade

## Create a user account
    sudo adduser username

## Tools
    sudo apt install fish -y
    sudo apt install net-tools -y

## GUI
    sudo apt install lightdm -y
    sudo apt install ubuntu-desktop -y
    sudo systemctl start lightdm.service
    sudo service lightdm start

## Installing ssh in Ubuntu
    sudo apt-get install openssh-client
    sudo systemctl enable ssh
    sudo ufw allow ssh
    sudo systemctl status ssh

## Webmin
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

Webmin set password

    sudo /usr/share/webmin/changepass.pl /etc/webmin root [new password]

https://[your server's IP]:10000/

refer : https://phoenixnap.com/kb/install-webmin-on-ubuntu
