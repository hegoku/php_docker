php-7.2.28

PHP Ext：

```
swoole-4.4.16 --enable-mysqlnd --enable-sockets
mcrypt-1.0.2
redis-4.3.0
mongodb-1.5.3
rdKafka
gd
zip
opcache
```

Software:

```
ssmtp
```

php-fpm

```
docker run --name name -p your_port:9000 -v your_web_dir:/var/www/html -v your_php_ini_file:/usr/local/etc/php/php.ini -v your_fpm_config_file:/usr/local/etc/php-fpm.d/file.conf hegoku/php
```

php-cli

```
docker run --name name -v your_web_dir:/var/www/html -v your_php_ini_file:/usr/local/etc/php/php.ini hegoku/php hegoku/php /usr/local/bin/php /var/www/html/a.php
```
