FROM php:apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli && docker-php-ext-install opcache && docker-php-ext-enable opcache && docker-php-ext-install pdo_mysql && docker-php-ext-enable pdo_mysql
RUN a2enmod rewrite

# Install Xdebug
RUN pecl -q install xdebug \
    && docker-php-ext-enable xdebug

# Install composer globally
RUN curl -sSL https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# Update ini file for Xdebug using PhpStorm
RUN echo "xdebug.remote_enable = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart = 1" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey = \"PHPSTORM\"" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_host = docker.for.win.localhost" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port = 9000" \
        >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini