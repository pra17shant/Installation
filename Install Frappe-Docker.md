# Frappe Docker - All Commands


### Installation of Docker & Docker Compose

Uninstall Old version of docker or docker-engine. If you have it installed, first uninstall it.

```
sudo apt update
sudo apt remove docker docker-engine [docker.io](http://docker.io/) 2>/dev/null
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
sudo apt install docker-ce docker-ce-cli [containerd.io](http://containerd.io/) docker-compose-plugin
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

## Copy frappe_docker repo
```
cd ~/
git clone https://github.com/frappe/frappe_docker
cd frappe_docker
```
___

## Create a directory for resources and configuration 
```
mkdir ~/gitops
```

### Install Treaefik and Configuration
```
echo 'TRAEFIK_DOMAIN=traefik.example.com'> ~/gitops/traefik.env
echo 'EMAIL=admin@example.com' >> ~/gitops/traefik.env
echo 'HASHED_PASSWORD='$(openssl passwd -apr1 Anand | sed 's/\$/\\\$/g') >> ~/gitops/traefik.env
```
* Change the domain from traefik.example.com to the one used in production. DNS entry needs to point to the Server IP.
* Change the letsencrypt notification email from admin@example.com to correct email.
* Change the password from changeit to more secure.
* env file generated at location ~/gitops/traefik.env will look like following:

### Now Deploy the traefik container with letsencrypt SSL
```
docker compose --project-name traefik \
--env-file ~/gitops/traefik.env \
-f overrides/compose.traefik.yaml \
-f overrides/compose.traefik-ssl.yaml up -d
```
### Now Deploy the traefik container without SSL Or Access localy then use below
```
docker compose --project-name traefik \
--env-file ~/gitops/traefik.env \
-f overrides/compose.traefik.yaml up -d
```

## Install MariaDB

```
echo "DB_PASSWORD=SetYourStrongPassword" > ~/gitops/mariadb.env
```
* SetYourStrongPassword To change and set password

### Up MariaDB container
```
docker compose --project-name mariadb --env-file ~/gitops/mariadb.env -f overrides/compose.mariadb-shared.yaml up -d
```
___
## Create the persistent volume: (If Required)

```
sudo mkdir -p /mnt/data/sites
```
* Set the required permissions

```
sudo chmod 775 -R /mnt/data
sudo chown -R $USER:docker /mnt/data
```
* Now create the docker volume for sites
```
docker volume create --driver local \
     --opt type=none \
     --opt device=/mnt/data/sites \
     --opt o=bind sites
```
____
## Now Finally frappe docker Installation start
### Note: 
* *"jay.env"* is my envoirment you can chenge occurdingly where i wrote this
* *"ToSetYourPassword"* Chenge this wording your need's.
* demo1.example.com\`, \`demo2.example.com\ You Can Change this line
```
cp example.env ~/gitops/jay.env
sed -i 's/DB_PASSWORD=123/DB_PASSWORD=ToSetYourPassword/g' ~/gitops/jay.env
sed -i 's/DB_HOST=/DB_HOST=mariadb-database/g' ~/gitops/jay.env
sed -i 's/DB_PORT=/DB_PORT=3306/g' ~/gitops/jay.env
echo 'ROUTER=jay' >> ~/gitops/jay.env
echo "SITES=\`demo1.example.com\`, \`demo2.example.com\`" >> ~/gitops/jay.env
echo "BENCH_NETWORK=jay" >> ~/gitops/jay.env
```
### Now Compose recentrly creatted yml files (With SSL)
### Note: 
* *"jay.env"*  or jay & jay.yaml is my envoirment you can chenge occurdingly where i wrote this
```
docker compose --project-name jay \
--env-file ~/gitops/jay.env \
-f compose.yaml \
-f overrides/compose.redis.yaml \
-f overrides/compose.multi-bench.yaml \
-f overrides/compose.multi-bench-ssl.yaml config > ~/gitops/jay.yaml
```
### Now Compose recentrly creatted yml files (Without SSL OR Local Setup)
#### Note: 
* *"jay.env"*  or jay & jay.yaml is my envoirment you can chenge occurdingly where i wrote this
```
docker compose --project-name jay \
--env-file ~/gitops/jay.env \
-f compose.yaml \
-f overrides/compose.redis.yaml \
-f overrides/compose.multi-bench.yaml config > ~/gitops/jay.yaml
```

### Finally Up the container using yaml file.
```
docker compose --project-name jay -f ~/gitops/jay.yaml up -d
```
### Create Site
#### Note:
* Replace jay to your name & replace below also
* Site Name: demo1.example.com 
* DB Pass: StrongPassw0rd
* admin Pass: pk@@123
```
docker exec -it  jay-backend-1 /bin/bash
docker compose --project-name jay exec backend \
bench new-site demo1.example.com  --no-mariadb-socket --mariadb-root-password StrongPassw0rd --install-app erpnext --admin-password pk@@123
docker compose --project-name jay exec backend \
bench --site demo1.example.com migrate
docker compose --project-name jay exec backend \
bench --site demo1.example.com -install-app hrms
```
## Finally Restart docker 
```
sudo docker compose --project-name capgrid -f ~/gitops/jay.yaml restart
```
## Some Basic Docker Command
* To List container
  ```
  docker ps
  ```
* For Up Any container using yaml then
  ```
  sudo docker compose --project-name capgrid -f ~/gitops/jay.yaml up -d
  ```
* For Down container using yaml then
  ```
  sudo docker compose --project-name capgrid -f ~/gitops/capgrid.yaml down
  ```
* For Remove container using id then
  ```
  sudo docker rm <container-id 1> <container-id 2> <container-id 3> ... <container-id n>
  ```
* For Stoping container using id then
```
sudo docker stop <container-id 1> <container-id 2> <container-id 3> ... <container-id n>
```
  
