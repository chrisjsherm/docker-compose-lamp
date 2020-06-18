# LAMP stack built with Docker Compose

A basic LAMP stack environment built using Docker Compose. It consists of the following:

- PHP
- Apache
- MySQL
- phpMyAdmin
- redis

Use appropriate php version as needed:

- 5.4.x
- 5.6.x
- 7.1.x
- 7.2.x
- 7.3.x
- 7.4.x

## Installation

- Clone this repository on your local computer
- Configure .env as needed
- Run the `docker-compose` command

```shell
git clone https://github.com/sprintcube/docker-compose-lamp.git
cd docker-compose-lamp/
cp sample.env .env
// modify sample.env as needed
docker-compose up -d
// visit localhost
```

Your LAMP stack is now ready!! You can access it via `http://localhost`.

## Configuration and Usage

### Configuration

This package comes with default configuration options. You can modify them by creating `.env` file in your root directory.
To make it easy, just copy the content from `sample.env` file and update the environment variable values per your needs.

### Configuration Variables

There are the following configuration variables available. You can customize them by overwriting in your own `.env` file.

---

#### PHP

---

_**PHPVERSION**_
Is used to specify which PHP Version you want to use. Defaults always to latest PHP Version.

_**PHP_INI**_
Define your custom `php.ini` modification to meet your requirments.

---

#### Apache

---

_**DOCUMENT_ROOT**_

It is a document root for Apache server. The default value for this is `./www`. All your sites will go here and will be synced automatically.

_**VHOSTS_DIR**_

This is for virtual hosts. The default value for this is `./config/vhosts`. You can place your virtual hosts conf files here.

> Make sure you add an entry to your system's `hosts` file for each virtual host.

_**APACHE_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/apache2`.

---

#### Database

---

_**DATABASE**_
Define which MySQL or MariaDB Version you would like to use.

_**MYSQL_DATA_DIR**_

This is MySQL data directory. The default value for this is `./data/mysql`. All your MySQL data files will be stored here.

_**MYSQL_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/mysql`.

## Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

- rewrite
- headers

> If you want to enable more modules, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

#### Connect via SSH

You can connect to web server using `docker-compose exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker-compose exec webserver bash
```

## PHP

The installed version of depends on your `.env`file.

#### Extensions

By default following extensions are installed.
May differ for PHP Verions <7.x.x

- mysqli
- pdo_sqlite
- pdo_mysql
- mbstring
- zip
- intl
- mcrypt
- curl
- json
- iconv
- xml
- xmlrpc
- gd

> If you want to install more extensions, update `./bin/webserver/Dockerfile`.
> You have to rebuild the docker image by running `docker-compose build` and restart
> the docker containers after installing new extensions.

## phpMyAdmin

phpMyAdmin is configured to run on port 8080. Use following default credentials.

http://localhost:8080/  
username: root  
password: tiger

## Redis

It comes with Redis. It runs on default port `6379`.

## Modify this stack before deploying to production

In Production you should modify, at a minimum, the following:

- php handler: mod_php=> php-fpm
- secure mysql users with proper source IP limitations

## Deployment

Each time you merge a commit to master, a GitHub Actions workflow copies the
following directories to the remote server.

- config
- www

### Secrets

The address of the remote server is defined in this repository's GitHub Secrets.
The credentials for connecting the the remote server are defined there as well.
