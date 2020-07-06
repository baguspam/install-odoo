# INSTALL ODOO 12 - UBUNTU 20.04

> Update check ubuntu
- sudo apt-get update
- sudo apt-get upgrade
- sudo apt install git python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less
<br><br>
> Install postgresql and configure
- sudo apt-get install postgresql
- sudo su - postgres
- su - postgres
- createuser --interactive --pwprompt
- (input your username and password)
- exit
<br><br>
> Install wkhtmlpdf
- wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
- sudo apt install ./wkhtmltox_0.12.5-1.bionic_amd64.deb
<br><br>
> Install pyhton 3.6.9 (because python 3.8 default from ubuntu 20.04 not recomended)
- sudo su
- cd /usr/src
- sudo wget https://www.python.org/ftp/python/3.6.9/Python-3.6.9.tgz
- sudo tar xzf Python-3.6.9.tgz
- sudo apt-get install libssl-dev
- cd Python-3.6.9
- sudo ./configure --enable-optimizations
- sudo make altinstall
(for check python version 3.6.9)
- python3.6 -V 
- sudo pip3.6 install virtualenv
<br><br>
> Install and configure odoo12 (note: it's git clone from odoo12 version latest (recomended) because new version many for bugs and error for installation)
- sudo useradd -m -d /opt/odoo12 -U -r -s /bin/bash odoo12
- cd /opt/odoo12
- python3.6 -m venv odoo-venv
- sudo su - odoo12
- git clone https://www.github.com/odoo/odoo --depth 1 --branch 12.0 /opt/odoo12/odoo
- source odoo-venv/bin/activate
- pip3.6 install wheel
- pip3.6 install -r odoo/requirements.txt
- deactivate
- mkdir /opt/odoo12/odoo-addons
- exit
<br><br>
> Setup Config file for odoo12
- sudo cp /opt/odoo12/odoo/debian/odoo.conf /etc/odoo12.conf
- sudo nano /etc/odoo12.conf
- Edit it as follows and don't forget change_password_master_admin_database, change_username_postgre, and change_password_postgre :
> [options]<br>
> ; This is the password that allows database operations:<br>
> admin_passwd = change_password_master_admin_database<br>
> db_host = localhost<br>
> db_port = 5432<br>
> db_user = change_username_postgre<br>
> db_password = change_password_postgre<br>
> addons_path = /opt/odoo12/odoo/addons,/opt/odoo12/odoo-addons<br>
- Crtl + x (for save and exit)
<br><br>
> Setup service for odoo12
- sudo nano /etc/systemd/system/odoo12.service
- Copy and paste the following configuration :
> [Unit]<br>
> Description=Odoo12<br>
> Requires=postgresql.service<br>
> After=network.target postgresql.service<br>
> <br>
> [Service]<br>
> Type=simple<br>
> SyslogIdentifier=odoo12<br>
> PermissionsStartOnly=true<br>
> User=odoo12<br>
> Group=odoo12<br>
> ExecStart=/opt/odoo12/odoo-venv/bin/python3 /opt/odoo12/odoo/odoo-bin -c /etc/odoo12.conf<br>
> StandardOutput=journal+console<br>
> <br>
> [Install]<br>
> WantedBy=multi-user.target<br>
- Crtl + x (for save and exit)
<br><br>
> Reload deamon, start service, and status
- sudo systemctl daemon-reload
- sudo systemctl start odoo12 (for running always odoo12 on the startup service)
- sudo service odoo12 start (for running odoo12 manualy, service stop automatic while restart)
- sudo service odoo12 status (check log status service odoo)
- sudo service odoo12 stop (stop service odoo12)
- sudo service odoo12 restart (restart service odoo12)
<br><br>
> Reference for documentation
- <a href="https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/">https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/</a>
- <a href="https://www.getopenerp.com/install-odoo-12-on-ubuntu-18-04/">https://www.getopenerp.com/install-odoo-12-on-ubuntu-18-04/</a>
- <a href="https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line">https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line</a>

Credit by : Bagus P.
