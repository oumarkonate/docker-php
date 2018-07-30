DOCKER-PHP
==
PHP applications using: &nbsp;Nginx, &nbsp;PHP7-FPM, &nbsp;PhpMyAdmin, &nbsp;MariaDB
<br/>
Compose file: version 3
<br/>
PHP Extension: memcached, opcache, pdo_mysql, gd, iconv, mcrypt, intl, mbstring, curl, zip, json, xdebug

Installation
-
* First, clone this repository:
```
git clone https://github.com/oumarkonate/docker-php.git
```

* Next, add the following line in file /etc/hosts:
```
127.0.0.1 php.localhost www.php.localhost
```
Restart the network service by the command:
```
/etc/init.d/networking restart
```

* Then, go to folder "docker-php" and run:
```
docker-compose up -d
```

* Go to the application on the following url: ```http://php.localhost```

Run your project
-
Put your index file into ```public``` directory located into root directory.
<br/>
If your index file is located into directory ```public/path-to-index-file/indexFile``` then run your project by accessing to url ```http://php.localhost/path-to-index-file```

Access to PhpMyAdmin
-
You can access phpmyadmin from the url: ```http://php.localhost:8001```
* _Username: dev_
* _Password: dev123_

Show docker processes
-
You can view the docker processes by running the following command line:
```
docker ps
```
Command output:
```
CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                            NAMES
41cd17475c54        docker-php_php          "docker-php-entrypoi…"   4 hours ago         Up 38 minutes       9000/tcp                         docker-php_php7
78c9d363738f        phpmyadmin/phpmyadmin   "/run.sh phpmyadmin"     4 hours ago         Up 38 minutes       9000/tcp, 0.0.0.0:8001->80/tcp   docker-php_pma
f1048e6a4735        mariadb:latest          "docker-entrypoint.s…"   4 hours ago         Up 38 minutes       0.0.0.0:3306->3306/tcp           docker-php_mariadb
f75ff6210ada        nginx:latest            "nginx -g 'daemon of…"   4 hours ago         Up 38 minutes       0.0.0.0:80->80/tcp               docker-php_nginx
```


Access to a container
-
You can access your container via the command line:
```
docker exec -it CONTAINER_NAME bash
```

Example: to access the php7 container
```
docker exec -it docker-php_php7 bash
```

Note
-

* Stop containers by running the following command:
```
docker-compose stop
```

* Rebuild containers by running the following command:
```
docker-compose build
```


