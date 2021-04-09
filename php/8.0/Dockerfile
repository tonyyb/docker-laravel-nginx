FROM php:8.0-fpm-alpine

MAINTAINER tonyyb <dev@tony.botalla.me>

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
        imagemagick-dev \
        freetype-dev  \
        gmp-dev \
        libtool \
        libxml2-dev \
        postgresql-dev \
        sqlite-dev \
        libpng-dev \
        libmcrypt-dev \
        libjpeg-turbo-dev \
        zlib-dev \
        openldap-dev \
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
        rsync \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv \
    && git clone https://github.com/Imagick/imagick /tmp/imagick; cd /tmp/imagick/; phpize && ./configure; make; make install; cd /tmp; rm -rf imagick \
    && docker-php-ext-enable imagick \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && docker-php-ext-configure exif \
    && docker-php-ext-install \
        bcmath \
        exif \
        gd \
        gmp \
        intl \
        ldap \
        mysqli \
        pcntl \
        pdo_mysql \
        pdo_pgsql \
        pdo_sqlite \
        pgsql \
        soap \
        tokenizer \
        zip \
        xml \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && wget https://getcomposer.org/installer && cat installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && cat installer | php -- --1 --install-dir=/usr/local/bin/ --filename=composer1 \
    && rm installer \
    && apk del -f .build-deps



# Fix for iconv: https://github.com/docker-library/php/issues/240
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

WORKDIR /var/www
