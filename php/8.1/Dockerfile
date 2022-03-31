FROM php:8.1-fpm-alpine

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
        libjpeg-turbo-dev 
    RUN apk add --no-cache \
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
        yarn \
        libzip-dev \
        rsync \
        openldap-dev
    RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv 
    RUN pecl install imagick redis mongodb
    RUN docker-php-ext-enable imagick redis mongodb
    RUN docker-php-ext-configure exif 
    RUN docker-php-ext-install \
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
        zip \
        xml
    RUN apk add --no-cache libwebp-dev libpng-dev libjpeg-turbo-dev freetype-dev
    RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp 
    RUN wget https://getcomposer.org/installer && cat installer | php -- --install-dir=/usr/local/bin/ --filename=composer 
    RUN cat installer | php -- --1 --install-dir=/usr/local/bin/ --filename=composer1 
    RUN rm installer 
    RUN apk del -f .build-deps

WORKDIR /var/www
