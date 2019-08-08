FROM php:apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli && docker-php-ext-install opcache && docker-php-ext-enable opcache && docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql
RUN a2enmod rewrite
