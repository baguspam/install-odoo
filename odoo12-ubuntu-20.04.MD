# INSTALL ODOO 12 - UBUNTU 20.04

> Update check ubuntu
- sudo apt-get update
- sudo apt-get upgrade
- sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less

> Install postgre
- sudo apt-get install postgresql
- sudo su - postgres

> Install wkhtmlpdf
- wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
- sudo apt install ./wkhtmltox_0.12.5-1.bionic_amd64.deb

> Install pyhton 3.6.8
- sudo su
- cd /usr/src
- sudo wget https://www.python.org/ftp/python/3.6.8/Python-3.6.8.tgz
- sudo tar xzf Python-3.6.8.tgz
- sudo apt-get install libssl-dev
- cd Python-3.6.8
- sudo ./configure --enable-optimizations
- sudo make altinstall
(for check python version 3.6.8)
- python3.6 -V 
- sudo pip3 install virtualenv

> Install and configure odoo
- sudo useradd -m -d /opt/odoo12 -U -r -s /bin/bash odoo12
- cd /opt/odoo12
- virtualenv odoo-venv -p python3.6
- sudo su - odoo12
- git clone https://www.github.com/odoo/odoo --depth 1 --branch 12.0 /opt/odoo12/odoo
- source odoo-venv/bin.activate
- pip install -r odoo/requirements.txt



