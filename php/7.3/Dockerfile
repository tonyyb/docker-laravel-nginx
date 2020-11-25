FROM php:7.3-fpm-alpine

MAINTAINER tonyyb <dev@tony.botalla.me>

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
        libpng-dev \
        libmcrypt-dev \
        freetype-dev  \
        libjpeg-turbo-dev \
        zlib-dev \
    && apk add --no-cache \
        bash \
        curl \
        git \
        imagemagick \
        mysql-client \
        openssh-client \
        postgresql-libs \
        libintl \
        icu \
        icu-dev \
        nodejs \
        nodejs-npm \
        yarn \
        libzip-dev \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-configure exif \
    && docker-php-ext-install \
        bcmath \
        curl \
        iconv \
        mbstring \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pcntl \
        tokenizer \
        xml \
        intl \
        exif \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && wget https://getcomposer.org/installer && cat installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && cat installer | php -- --1 --install-dir=/usr/local/bin/ --filename=composer1 \
    && rm installer \
    && apk del -f .build-deps

# Fix for iconv: https://github.com/docker-library/php/issues/240
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

WORKDIR /var/www
