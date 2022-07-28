FROM php:8.1-fpm
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

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
  && pecl install imagick && docker-php-ext-enable imagick \
  && rm -rf /var/lib/apt/lists/*

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
