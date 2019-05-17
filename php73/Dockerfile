FROM php:7.3.5-fpm-alpine3.9

RUN apk add --no-cache --virtual .build-deps \
        libxml2-dev \
        shadow \
        autoconf \
        g++ \
        make \
        libmcrypt-dev \
    && apk add libstdc++ libmcrypt \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis \
    && pecl install channel://pecl.php.net/mcrypt-1.0.2 \ 
    && pecl install mongodb \
    && docker-php-ext-enable redis mcrypt mongodb \
    && docker-php-ext-install sockets \
    && curl -fsSL 'https://pecl.php.net/get/swoole-4.3.4.tgz' -o swoole-4.3.4.tgz \
    && mkdir -p swoole \
    && tar -xf swoole-4.3.4.tgz -C swoole --strip-components=1 \
    && rm swoole-4.3.4.tgz \
    && ( \
        cd swoole \
        && phpize \
        && ./configure --enable-mysqlnd --enable-sockets \
        && make -j "$(nproc)" \
        && make install \
    ) \
    && rm -r swoole \
    && docker-php-ext-enable swoole \
    && apk del .build-deps

