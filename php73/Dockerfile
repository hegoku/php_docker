FROM php:7.3.13-fpm-alpine3.11

RUN apk add --no-cache --virtual .build-deps \
        libxml2-dev \
        shadow \
        autoconf \
        g++ \
        make \
        libmcrypt-dev \
        librdkafka-dev \
        libpng-dev \
        libzip-dev \
    && apk add libstdc++ libmcrypt librdkafka ssmtp libpng libzip \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis \
    && pecl install channel://pecl.php.net/mcrypt-1.0.2 \ 
    && pecl install mongodb \
    && docker-php-ext-enable redis mcrypt mongodb \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && curl -fsSL 'https://pecl.php.net/get/swoole-4.4.14.tgz' -o swoole.tgz \
    && mkdir -p swoole \
    && tar -xf swoole.tgz -C swoole --strip-components=1 \
    && rm swoole.tgz \
    && ( \
        cd swoole \
        && phpize \
        && ./configure --enable-mysqlnd --enable-sockets \
        && make -j "$(nproc)" \
        && make install \
    ) \
    && rm -r swoole \
    && docker-php-ext-enable swoole \
    && pecl install rdkafka \
    && docker-php-ext-enable rdkafka \
    && apk del .build-deps

