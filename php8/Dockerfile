# Build using docker buildx build . --platform linux/amd64,linux/arm64 -t benatherton/php8 --push
FROM php:8.4-fpm
LABEL maintainer="Ben Atherton <ben@benatherton.com>"

# Packages
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    # needed for gd
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    # needed for zip
    zip \
    libzip-dev \
    # needed for imagick
    libmagickwand-dev \
    imagemagick \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    build-essential \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/Imagick/imagick.git --depth 1 /tmp/imagick && \
    cd /tmp/imagick && \
    git fetch origin master && \
    git switch master && \
    cd /tmp/imagick && \
    phpize && \
    ./configure && \
    make && \
    make install && \
    apt-get remove -y git && \
    docker-php-ext-enable imagick

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli opcache pdo_mysql zip exif intl

# Install Intl
RUN docker-php-ext-configure intl

# Install GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j "$(nproc)" gd

# Install WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar && mv wp-cli.phar /bin/wp
