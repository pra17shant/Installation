---
Install ERPNext ERP on Ubuntu 22.04
---
```
erp@ERP-Next:~$ lsb_release -a

Distributor ID: Ubuntu
Description:    Ubuntu 22.10
Release:        22.10
Codename:       kinetic
```
---
Install ERPNext on Ubuntu 22.04
----
```
sudo apt update
sudo apt -y upgrade
sudo reboot
```
---
Step 1: Create a new user – (bench user)
---
Syntax:
```
sudo adduser [frappe-user]
usermod -aG sudo [frappe-user]
su [frappe-user] 
cd /home/[frappe-user]
```
In My Case:
```
sudo adduser erp
usermod -aG sudo erp
su erp 
cd /home/erp
```
---
Step 2: Install Required Packages
---
* GIT
* Python version 3.10+
* Python Virtual Environment
* Software Properties Common
* MariaDB
* Redis Server
* And other Mainer packages Like(xvfb, libfontconfig, wkhtmltopdf, libmysqlclient-dev)
```
sudo apt install git python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils python3.10-venv software-properties-common mariadb-server mariadb-client redis-server libfontconfig wkhtmltopdf libmysqlclient-dev -y
```
---
Step 3: Configure MYSQL Server
---
**Server Setup:**
```
sudo mysql_secure_installation
```
**Following Answaer as is**
```
Enter current password for root (enter for none): 
OK, successfully used password, moving on...
Switch to unix_socket authentication [Y/n] Y
Change the root password? [Y/n] Y
Remove anonymous users? [Y/n] Y
Disallow root login remotely? [Y/n] n
Remove test database and access to it? [Y/n] Y
Reload privilege tables now? [Y/n] Y
Cleaning up...
All done!
```

**Edit MYSQL default config file**

 Redirect The File Location
```
sudo nano /etc/mysql/my.cnf
```
**End Of The File Pase It as is:**
```
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
```
**Restart the MYSQL Server**
```
sudo service mysql restart
```
---
Install CURL, Node, NPM and Yarn
---
**Install Curl & NVM**
```
sudo apt install curl
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
```
**Copy The Terminal Line and past it again**
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```
**Set The Path Default**
```
source ~/.profile
```
**To Check NVM Version and chose (Latest LTS Version Number)**

```
nvm ls-remote

```
**In My Case  v18.13.0   (Latest LTS: Hydrogen)**
**Finally we install Success NVM & Node **
```
nvm install 18.13.0
```

**Now Install NPM**
```
sudo apt-get install npm
```
**Install Yarn**
```
sudo npm install -g yarn
```
**Install Frappe Bench**
```
sudo pip3 install frappe-bench
```
If comes in ERROR Line Red Color Then Just Install Thwos packege missed-out I Got Error Like
![image](https://user-images.githubusercontent.com/99401472/212287803-105e6872-2584-4896-99a7-74239f98fc6c.png)

**So I solve Like using command**
```
sudo pip3 install jsonpatch
sudo pip3 install jsonschema
```
And Then again pass Install Frappe Bench comand:
```
sudo pip3 install frappe-bench
```
We Expect Only WARNING Message at the bottom of line like billow image
![image](https://user-images.githubusercontent.com/99401472/212287583-4190be67-f51d-442f-b05a-02aa99ded6f5.png)

To Check Bench Version First using
```
bench --version
```
I Got Bench Vesrion
![image](https://user-images.githubusercontent.com/99401472/212288605-70646a4d-3a51-438f-b292-5a631e6f7088.png)

**Now Initialize Frappe Bench and its Packege Using**
```
bench init --frappe-branch version-14 frappe
```
I Got 
![image](https://user-images.githubusercontent.com/99401472/212289869-48249717-6643-48f6-a6df-9e4c6f33d9d2.png)

In My Case I Create frappe folder in home directory

Switch directories into the Frappe directory using
![image](https://user-images.githubusercontent.com/99401472/212290430-5fc69197-e03c-4bc2-a936-8add79beb94f.png)
```
cd frappe
```
In My Case I Got my user get Exicute permission if you not then go ahed next command otherwise skip it
```
chmod -R o+rx /home/[frappe]
```
**Create a First New Site**
```
bench new-site <site-name> --db-name <Database-Name>
```
In My Case
```
bench new-site demo.erp.com --db-name demo
```
Give the DB Password and Wait till ask To set administrator password:

---
Install ERPNext and other Apps
---
**Required Apps For ERPNext**
* payments
* erpnext
* India-Complaince (If Indian Base Site Then I recommended this also otherwise skipp it) https://github.com/resilient-tech/india-compliance.git

**Now Start To Get App**
```
bench get-app payments
bench get-app --branch version-14 erpnext 
bench get-app --branch version-14 https://github.com/resilient-tech/india-compliance.git
```
**Install all the apps on our site**
```

```
```
bench --site demo.erp.com install-app payments
bench --site demo.erp.com install-app erpnext
bench --site demo.erp.com install-app india_compliance
```





























