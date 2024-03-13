# Install Frappe-Docker For Devloper

### Installation of Docker & Docker Compose

Uninstall Old version of docker or docker-engine. If you have it installed, first uninstall it.

```
sudo apt update
sudo apt remove docker docker-engine docker.io 2>/dev/null
```

### Install packages to allow apt to use a repository over HTTPS

```
sudo apt -y install lsb-release gnupg apt-transport-https ca-certificates curl software-properties-common
```

### Add Docker’s official GPG key

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg
```

### Add stable repository
```
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
### Install docker CE

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
### Ensure OpenSSL is installed
```
sudo apt install openssl
```
### Start and enable the service:** 
```
sudo systemctl start docker && sudo systemctl enable docker
```
____
## Create User and docker group ( if you needed )

```
sudo usermod -aG docker $USER
newgrp docker
```
___
* Clone Frappe Docker Public Repo on your System
```
git clone https://github.com/frappe/frappe_docker.git <your_projectname>
```
My Case
```
git clone https://github.com/frappe/frappe_docker.git gurukrupa_docker
```
* After Cloned GO Inside that folder and copy some Folder using following command
```
cd gurukrupa_docker;
cp -R devcontainer-example .devcontainer;
cp -R development/vscode-example development/.vscode;
```
* Now Open VSCode using command or directly click on icon
```
code .
```
* After Open VSCode (Shortcut: Ctrl+Shift+p) or click on View and select Command pallet then Select. **Reopen in devcontainer** and Wait for standing up container.
* After Done Process you Already inside the container then create file
  ```
  touch apps.json
  ```
* Open This file and add your application like below code
* Note: If You Have Private repo then use personal access (PAT) token for cloning you aap
  Public Repo:
  ```
  [
  {
    "url": "https://github.com/frappe/hrms.git",
    "branch": "version-14"
  },
  {
    "url": "https://github.com/frappe/erpnext.git",
    "branch": "version-14"
  }
  ]
  ```
  Private Repo:
  Suppose i genrate PAT token (ghp_hpgEkjtvbW4HLcyTawqsfvktb5c1DF3SytHX) and repo HTTPS path is like (https://github.com/git_user/xyz.git) then build like bellow.

  ```
    [
  {
    "url": "https://git_user:ghp_hpgEkjtvbW4HLcyTawqsfvktb5c1DF3SytHX@github.com/git_user/xyz.git",
    "branch": "main"
  },
  {
    "url": "https://git_user:ghp_hpgEkjtvbW4HLcyTawqsfvktb5c1DF3SytHX@github.com/git_user/abc.git",
    "branch": "main"
  }
  ]
  ```
* Once Ready apps.json file then execute following command.
* For Help with installer.py:</br>
  -h, --help            show this help message and exit</br>
  -j APPS_JSON, --apps-json APPS_JSON Path to apps.json, default: apps-example.json</br>
  -b BENCH_NAME, --bench-name BENCH_NAME  Bench directory name, default: frappe-bench</br>
  -s SITE_NAME, --site-name SITE_NAME Site name, should end with .localhost, default: development.localhost</br>
  -r FRAPPE_REPO, --frappe-repo FRAPPE_REPO frappe repo to use, default: https://github.com/frappe/frappe</br>
  -t FRAPPE_BRANCH, --frappe-branch FRAPPE_BRANCH frappe repo to use, default: version-14</br>
  -p PY_VERSION, --py-version PY_VERSION python version, default: Not Set</br>
  -n NODE_VERSION, --node-version NODE_VERSION node version, default: Not Set</br>
  -v, --verbose         verbose output</br></br>
* If You change python version and node version then use (-p 3.11.4 -n v18 )
  ```
   ./installer.py -t develop -j apps.json -v
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/d4e0af89-f078-4ed4-8de7-280ec9ec5b61)

* I got this error then press y for rollback
  ![image](https://github.com/pra17shant/Installation/assets/99401472/9cc1bc43-dd37-43d5-9e00-cba86f4445d0)

* Resolve version error
  ```
  ./installer.py -t develop -s gurukrupa.local -b gurukrupa_bench -n v18 -j apps.json -v
  ```
* Once Install with you inside the your devlopment container
  ```
  bench start
  ```
* Note:
  if you setup everything then make sure please register your site in hosts file
  in linux
  ```
  sudo nano etc/hosts
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/ef9fda55-3b45-468a-8195-c9dbb6a70fea)

  
