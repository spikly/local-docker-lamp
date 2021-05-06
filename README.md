# LAMP Docker Stack

A container with Apache, PHP and MariaDB designed for fast setup and configuration of a local dev environment.

Place `docker-compose.yml` and the `localhost` folder into the root directory of your local website folder.

## Configuration

Before running the container, configure the LAMP stack to your liking.

#### PHP
Configuration location: `localhost/config/php/local.ini`

Example configuration:

```
error_reporting=E_ALL & ~E_DEPRECATED & ~E_STRICT & ~E_NOTICE
date.timezone="Europe/London"
memory_limit=512M
post_max_size=10M
upload_max_filesize=10M
```

#### Apache Virtual Hosts
Configuration location: `localhost/config/apache/vhosts.conf`

Example configuration:

```
<VirtualHost *:80>
	DocumentRoot "/var/www/html" 
	ServerName localhost
</VirtualHost>

<VirtualHost *:80> 
	DocumentRoot "/var/www/html/project1folder" 
	ServerName project1.local
</VirtualHost>

<VirtualHost *:80> 
	DocumentRoot "/var/www/html/project2folder" 
	ServerName project2.local
</VirtualHost>
```

#### MariaDB Root Password
Configuration location: `localhost/config/mariadb/root_password.txt`

Example configuration:

```
sup3r_s3cur3_passw0rd
```


## How to use

The following command should be run from the root directory of your local website folder (i.e. the location of `docker-compose.yml`).

### 1) Build the Docker container image:

```
docker image build --no-cache -f localhost/images/php-apache/Dockerfile -t php-7.3-apache .
```

### 2) Run the container:

```
docker stack deploy -c docker-compose.yml localdev
```

If you receive a notice that the current node is not a swarm manager, run the following command and then try the above command again:

```
docker swarm init
```

To stop the container:

```
docker stack rm localdev
```

To see which containers are currently running:

```
docker ps
```

