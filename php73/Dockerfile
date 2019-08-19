FROM php:7.3.8-fpm-alpine3.10

RUN apk add --no-cache --virtual .build-deps \
        libxml2-dev \
        shadow \
        autoconf \
        g++ \
        make \
        libmcrypt-dev \
        librdkafka-dev \
    && apk add libstdc++ libmcrypt librdkafka \
    && docker-php-ext-install pdo_mysql \
    && pecl install redis \
    && pecl install channel://pecl.php.net/mcrypt-1.0.2 \ 
    && pecl install mongodb \
    && docker-php-ext-enable redis mcrypt mongodb \
    && docker-php-ext-install sockets \
    && curl -fsSL 'https://pecl.php.net/get/swoole-4.4.3.tgz' -o swoole-4.4.3.tgz \
    && mkdir -p swoole \
    && tar -xf swoole-4.4.3.tgz -C swoole --strip-components=1 \
    && rm swoole-4.4.3.tgz \
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

