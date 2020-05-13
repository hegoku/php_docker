php-7.3.17

PHP Ext：

```
swoole-4.5.1 --enable-mysqlnd --enable-sockets
mcrypt-1.0.2
redis-5.2.2
mongodb-1.7.4
rdKafka-4.0.3
gd
zip
opcache
imagick-3.4.4
imagemagick-6.9.10.75
bcmath
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
