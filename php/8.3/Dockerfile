FROM php:8.3-fpm-alpine

MAINTAINER tonyyb <dev@tony.botalla.me>

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
    && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted \
        gnu-libiconv \
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
        zip \
        xml \
    && apk add --no-cache libwebp-dev libpng-dev libjpeg-turbo-dev freetype-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp \
    && wget https://getcomposer.org/installer && cat installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && rm installer

# Temporary hack : see https://github.com/Imagick/imagick/issues/643
# Commit 52ec37ff633de0e5cca159a6437b8c340afe7831 refer to : https://github.com/Imagick/imagick/releases/tag/3.7.0
RUN curl -L -o /tmp/imagick.tar.gz https://github.com/Imagick/imagick/archive/52ec37ff633de0e5cca159a6437b8c340afe7831.tar.gz \
    && tar --strip-components=1 -xf /tmp/imagick.tar.gz \
    && phpize \
    && ./configure \
    && make \
    && make install \
    && docker-php-ext-enable imagick

ARG INSTALL_MONGO_DB=false
RUN if [ ${INSTALL_MONGO_DB} = true ]; then \
      pecl install mongodb && \
      docker-php-ext-enable redis mongodb \
;fi

# Clean up
RUN apk del -f .build-deps \
    && rm -rf /tmp/*

WORKDIR /var/www
