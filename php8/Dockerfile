# Build using docker buildx build . --platform linux/amd64,linux/arm64 -t benatherton/php8 --push
FROM php:8.4.10-fpm-alpine3.22
LABEL maintainer="Ben Atherton <ben@benatherton.com>"

# Install runtime dependencies
RUN apk add --no-cache \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev \
    imagemagick \
    imagemagick-dev \
    icu-dev \
    curl \
    bash

# Install build dependencies, build extensions, then remove build deps
RUN apk add --no-cache --virtual .build-deps \
    git \
    g++ \
    make \
    autoconf \
    libtool \
    zlib-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j"$(nproc)" \
        gd \
        mysqli \
        opcache \
        pdo_mysql \
        zip \
        exif \
        intl \
    && git clone --depth 1 https://github.com/Imagick/imagick.git /tmp/imagick \
    && cd /tmp/imagick \
    && phpize \
    && ./configure \
    && make -j"$(nproc)" \
    && make install \
    && docker-php-ext-enable imagick \
    && rm -rf /tmp/imagick \
    && apk del .build-deps

# Install WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp
