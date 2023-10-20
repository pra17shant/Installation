# Install Frappe-Docker For Devloper
* Clone Frappe Docker Public Repo on your System
```
git clone https://github.com/frappe/frappe_docker.git <your_projectname>
```
My Case
```
git clone https://github.com/frappe/frappe_docker.git capgrid_docker
```
* After Cloned GO Inside that folder and copy some Folder using following command
```
cd capgrid_docker;
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
* For Help with installer.py:
  -h, --help            show this help message and exit
  -j APPS_JSON, --apps-json APPS_JSON Path to apps.json, default: apps-example.json
  -b BENCH_NAME, --bench-name BENCH_NAME  Bench directory name, default: frappe-bench
  -s SITE_NAME, --site-name SITE_NAME Site name, should end with .localhost, default: development.localhost
  -r FRAPPE_REPO, --frappe-repo FRAPPE_REPO frappe repo to use, default: https://github.com/frappe/frappe
  -t FRAPPE_BRANCH, --frappe-branch FRAPPE_BRANCH frappe repo to use, default: version-14
  -p PY_VERSION, --py-version PY_VERSION python version, default: Not Set
  -n NODE_VERSION, --node-version NODE_VERSION node version, default: Not Set
  -v, --verbose         verbose output
* If You change python version and node version then use (-p 3.11.4 -n v18 )
  ```
   ./installer.py -t develop -j apps.json -v
  ```
  ![image](https://github.com/pra17shant/Installation/assets/99401472/d4e0af89-f078-4ed4-8de7-280ec9ec5b61)

* I got this error then press y for rollback
  ![image](https://github.com/pra17shant/Installation/assets/99401472/9cc1bc43-dd37-43d5-9e00-cba86f4445d0)

* Resolve version error
  ```
  ./installer.py -t develop -s capgrid.local -b capgrid_bench -n v18 -j apps.json -v
  ```