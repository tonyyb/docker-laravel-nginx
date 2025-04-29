FROM php:8.3-fpm-alpine

RUN apk add --no-cache --virtual .build-deps \
        $PHPIZE_DEPS \
        curl-dev \
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
        imagemagick-dev \
        linux-headers \
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv \
    && pecl install imagick && docker-php-ext-enable imagick \
    && pecl install redis \
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
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del -f .build-deps \
    && rm -rf /tmp/*

RUN  echo "[xdebug]" > /usr/local/etc/php/conf.d/xdebug.ini && \
     echo "zend_extension=xdebug.so" >> /usr/local/etc/php/conf.d/xdebug.ini && \
     echo "xdebug.mode=coverage" >> /usr/local/etc/php/conf.d/xdebug.ini && \
     echo "xdebug.start_with_request=no" >> /usr/local/etc/php/conf.d/xdebug.ini

WORKDIR /var/www

