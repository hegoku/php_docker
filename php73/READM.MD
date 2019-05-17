php-7.3.5

swoole-4.3.4 --enable-mysqlnd --enable-sockets

mcrypt-1.0.2

redis-4.3.0

mongodb-1.5.3

php-fpm

```
docker run --name name -p your_port:9000 -v your_web_dir:/var/www/html -v your_php_ini_file:/usr/local/etc/php/php.ini -v your_fpm_config_file:/usr/local/etc/php-fpm.d/file.conf hegoku/php73
```

php-cli

```
docker run --name name -v your_web_dir:/var/www/html -v your_php_ini_file:/usr/local/etc/php/php.ini hegoku/php73 hegoku/php73 /usr/local/bin/php /var/www/html/a.php
```
