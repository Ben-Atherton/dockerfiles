FROM php:apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN a2enmod rewrite