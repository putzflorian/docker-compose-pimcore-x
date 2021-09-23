# Docker-Compose for Pimcore X (use only for developement)

### Checkout Repo
```bash
git clone https://github.com/putzflorian/docker-compose-pimcore-x.git
 ```
### Run Containers
```bash
# initialize and startup containers
docker-compose up -d
```
### Install Pimcore 
```bash
# get shell in running container and install pimcore x
docker exec -it pimcorex-php-fpm bash

COMPOSER_MEMORY_LIMIT=-1 composer create-project pimcore/skeleton .

#run installer
./vendor/bin/pimcore-install --mysql-host-socket=pimcorex-mariadb --mysql-username=pimcore --mysql-password=pimcore --mysql-database=pimcore 
 ```

### Use
After the installer is finished, you can open in your Browser:
* Frontend: http://localhost:9090
* Backend: http://localhost:9090/admin

### Debug with XDEBUG
* Add Cookie XDEBUG_SESSION to your Browser

#### File permissions 
On some machines docker has problems with the relative symlinked (static) files. Run those commands in your `pimcore-php` container 

```bash 
docker-compose exec -it pimcorex-php-fpm bash
chown www-data: . -R 
```

Optional set Permissions to 777 if you work on Windows in an WSL Environment
```bash
chmod 777 . -R 
```