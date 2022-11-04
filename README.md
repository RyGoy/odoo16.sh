# odoo16.sh
## This script can be run on a fresh ubuntu 20.04 server build. Tested on a virtual machine.

#!/bin/bash
echo "Welcome to the Odoo16 setup script for Ubuntu 20.04, <username> on line 3 must be changed to match your current username before or after running the script."
echo " ** begin ** "
export PATH=/home/username/.local/bin:$PATH
git clone https://github.com/odoo/odoo.git
sudo apt install python3-pip -y
sudo apt install python3-pip libldap2-dev libpq-dev libsasl2-dev
cd odoo
pip install -r requirements.txt
sudo apt install postgresql -y
sudo -u postgres createuser -s $USER
createdb $USER
wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.focal_amd64.deb
sudo apt install ./wkhtmltox_0.12.6-1.focal_amd64.deb -y
python3 odoo-bin --addons-path=addons -d mydb

