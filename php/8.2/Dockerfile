FROM php:8.2-fpm-alpine

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
        libzip-dev \
        rsync \
        openldap-dev \
        npm \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv \
    && pecl install imagick redis mongodb \
    && docker-php-ext-enable imagick redis mongodb \
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
        zip \
        xml \
    && apk add --no-cache libwebp-dev libpng-dev libjpeg-turbo-dev freetype-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && wget https://getcomposer.org/installer && cat installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && rm installer \
    && apk del -f .build-deps \
    && rm -rf /tmp/*

WORKDIR /var/www
