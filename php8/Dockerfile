FROM php:8.0.3-fpm
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
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/php/ext/imagick && \
  curl -fsSL https://github.com/Imagick/imagick/archive/448c1cd0d58ba2838b9b6dff71c9b7e70a401b90.tar.gz | tar xvz -C /usr/src/php/ext/imagick --strip 1

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli opcache pdo_mysql zip exif imagick

# Install GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j "$(nproc)" gd
