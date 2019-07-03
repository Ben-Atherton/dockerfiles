FROM php:apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli && docker-php-ext-install opcache && docker-php-ext-enable opcache
RUN a2enmod rewrite

# Add WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar && mv wp-cli.phar /bin/wp

# Add cron job to auto run WP-CLI
RUN echo "0 0 * * * root wp plugin update --all --allow-root --path=/var/www/html" >> /etc/crontab
