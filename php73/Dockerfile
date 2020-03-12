FROM php:7.3.15-fpm-alpine3.11

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
        imagemagick-dev \
    && apk add libstdc++ libmcrypt librdkafka ssmtp libpng libzip imagemagick \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis \
    && pecl install channel://pecl.php.net/mcrypt-1.0.2 \ 
    && pecl install mongodb \
    && pecl install imagick \
    && docker-php-ext-enable redis mcrypt mongodb imagick \
    && docker-php-ext-install sockets \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install opcache \
    && curl -fsSL 'https://pecl.php.net/get/swoole-4.4.16.tgz' -o swoole.tgz \
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

