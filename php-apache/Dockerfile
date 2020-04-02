FROM php:apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Packages
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  # needed for gd
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  && rm -rf /var/lib/apt/lists/*

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli && docker-php-ext-install opcache && docker-php-ext-enable opcache && docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql

# Install GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j "$(nproc)" gd

RUN a2enmod rewrite
