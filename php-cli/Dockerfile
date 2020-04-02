FROM php:7
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install Xdebug
RUN pecl -q install xdebug \
    && docker-php-ext-enable xdebug

# Install composer globally
RUN curl -sSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# update ini file for xdebug using phpstorm
RUN echo "xdebug.remote_enable = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey = \"PHPSTORM\"" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_host = docker.for.mac.localhost" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port = 9000" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
