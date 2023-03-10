---
Install ERPNext ERP on Ubuntu 22.10
---
To Check OS Version
```
erp@ERP-Next:~$ lsb_release -a
```
![image](https://user-images.githubusercontent.com/99401472/212861043-021582d2-c2dc-49dd-bbd1-eef5e327d985.png)

---
Install ERPNext on Ubuntu 22.10
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
* And other Mainer packages Like(libfontconfig, wkhtmltopdf, libmysqlclient-dev)
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
**Following Answer as is**
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
**End Of The File Past It as is:**
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
Step-4: Install CURL, Node, NPM and Yarn
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
**In My Case,  v18.13.0   (Latest LTS: Hydrogen)**
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
---
Step-5: **Install Frappe Bench**
---
```
sudo pip3 install frappe-bench
```
If it comes in ERROR Line Red Color Then Just Install Twos package missed-out I Got Error Like
![image](https://user-images.githubusercontent.com/99401472/212287803-105e6872-2584-4896-99a7-74239f98fc6c.png)

**So I solve like using command**
```
sudo pip3 install jsonpatch
sudo pip3 install jsonschema
```
And Then again pass Install Frappe Bench command:
```
sudo pip3 install frappe-bench
```
We Expect Only WARNING Message at the bottom of line like billow image
![image](https://user-images.githubusercontent.com/99401472/212287583-4190be67-f51d-442f-b05a-02aa99ded6f5.png)

To Check Bench Version First using properly installed or not
```
bench --version
```
I Got Bench Version
![image](https://user-images.githubusercontent.com/99401472/212288605-70646a4d-3a51-438f-b292-5a631e6f7088.png)

**Now Initialize Frappe Bench and its Package Using**
```
bench init --frappe-branch version-14 frappe
```
I Got 
![image](https://user-images.githubusercontent.com/99401472/212289869-48249717-6643-48f6-a6df-9e4c6f33d9d2.png)

In My Case, I Create frappe folder in home/user directory
![image](https://user-images.githubusercontent.com/99401472/212290430-5fc69197-e03c-4bc2-a936-8add79beb94f.png)

**NOTE: In My Case I Got my user Apply Read permission for other group, if you have then skipped it, otherwise go ahead next command.**
```
chmod -R o+rx /home/<User-Name>/[Your Frappe]
```
In My Case
```
chmod -R o+rx /home/erp/frappe
```

**Switch directories into the Frappe directory using**
```
cd /home/[user]/[frappe folder]
```
In My Case
```
cd /home/erp/frappe
```
___
### Time to use frappe framework with creating site installing app & All...!
___
Step-6: Create a First New Site
---
**(Make sure you are in the frappe folder, Otherwise bench command not work..!)**
```
bench new-site <site-name> --db-name <Database-Name>
```
In My Case
```
bench new-site demo.erp.com --db-name demo
```
Give the DB Password and Wait till ask To set administrator password:

---
Step-7: Download ERPNext and other required Apps
---
**List Required Apps For ERPNext**
* payments
* erpnext
* India-Complaince (If Indian Base Site Then I recommended this also otherwise skip it) https://github.com/resilient-tech/india-compliance.git

**Now Start To Download App from git**
```
bench get-app payments
bench get-app --branch version-14 erpnext 
bench get-app --branch version-14 https://github.com/resilient-tech/india-compliance.git
```
---
Step-8: Install all Downloaded apps on our site
---
```
bench --site <site-name> install-app <app-name.
```
In My Case
```
bench --site demo.erp.com install-app payments
bench --site demo.erp.com install-app erpnext
bench --site demo.erp.com install-app india_compliance
```
---
Step-9: Start Bench Server Process
---

If you have only one site then use following command for default site for particular bench.
```
bench use <Your Site Name>
```
In My Case
```
bench use demo.erp.com
```
and then Finally our site up check browser it's running or not
```
bench start
```
___
### Finally, we're done it Everything Now...! 
### Run Server and check browser it's working state or not, If Not then post your issue in erp form https://discuss.frappe.io/  and tag me. user: @pra17shant.

---
Steps For Production Server
---
Please Note no need to start bench manually if you're done this process it means your instance will start automatically even in the event you restart the server.
When this completes doing the settings, your instance is now in production mode and can be accessed using your IP, without needing to use the port

**Enable Scheduler**
```
bench --site [site-name] enable-scheduler
```
In My Case
```
bench --site demo.erp.com enable-scheduler
```
**Disable maintenance mode**
```
bench --site [site-name] set-maintenance-mode off
```
In My Case
```
bench --site demo.erp.com set-maintenance-mode off
```
**Setup production config**
```
sudo bench setup production [frappe-user (linux user)]
```
In My Case
```
sudo bench setup production erp
```
**Setup NGINX to apply the changes**
```
bench setup nginx
```
**Restart Supervisor and Launch Production Mode**
If you are prompted to save the new/existing config file, respond with a Y.
```
sudo supervisorctl restart all
sudo bench setup production [frappe-user]
```
In My Case
```
sudo supervisorctl restart all
sudo bench setup production erp
```
---
Steps For Multiple Site run in single bench (Devlopment server purpose Only)
---

Previous I have only one site name as "demo.erp.com", but I need to up in second site also in same bench and same port then must follow the steps else ignore.
Multitenant On for common_site_config.json file presented in site folder
```
bench config dns_multitenant on
```
or You can directly copy the content in **common_site_config.json** file present in site folder if you enable developer mode on then
```
"developer_mode": 1,
"dns_multitenant": true,
"pause_scheduler": 1,
```
*After that, create a 2nd site for same bench. (Follow Step-6 only) and finally run this command.
```
bench --site <site-name> add-to-hosts
```
In My Case
```
bench --site demo.erp.com add-to-hosts
bench --site demo1.erp.com add-to-hosts
```
**Note:** If your system running in local network with dhcp server and have local IP then replace 127.0.0.0 to your IP in /etc/hosts file.
to check linux IP using this command { ip -c a }
```
bench setup nginx
```
```
sudo service nginx reload
```
To access the sites in your browser useing like **1st site:** http://demo.erp.com:8000  **2nd site:** http://demo1.erp.com:8000  and so on so forth.

---
Steps For Installing SSL Certificate
---
Must Be...
1. Allow TCP 403 port.
2. Install snapd application.
3. Install certbot.
4. DNS Multitenant Setup process.
5. Valid Domain name preserve.
6. Need root permissions on your server.
7. Trusted Certificate Authority or a Self-Signed Certificate.

**If You Have all of this,then Now Lets Start**

Firewall Transmission Control Protocol(TCP)-403,HTTP Secure Port to be enable.
```
sudo ufw allow 443/tcp
```
Install snapd Application and update
```
sudo apt install snapd;
sudo snap install core;
sudo snap refresh core
```
If You already install SSL Certificate using certbot then remove first.
```
sudo apt-get remove certbot
```
Install certbot
```
sudo snap install --classic certbot;
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
Automatic SSL Installation NGINX
```
sudo certbot --nginx
```
If You Want to Install Manually than
```
sudo certbot certonly --nginx
```
Basically certbot auto renew certificate if not then this command to help you out
```
sudo certbot renew --dry-run
```
