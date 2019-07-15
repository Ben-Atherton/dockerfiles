FROM php:7
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install Xdebug
RUN pecl -q install xdebug \
    && docker-php-ext-enable xdebug

# Install composer globally
RUN curl -sSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# ini settings for Xdebug
RUN echo "xdebug.remote_enable = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini