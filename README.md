# Linux
Linux lab
## Basic comman:
    sudo apt update && sudo apt upgrade
or

    sudo apt-get update && sudo apt-get upgrade

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
