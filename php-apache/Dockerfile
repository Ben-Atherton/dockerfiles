FROM php:7.4-apache
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
  # needed for ModSecurity & OWASP ModSecurity CRS
  libapache2-mod-security2 \
  modsecurity-crs \
  # needed for imagick
  libmagickwand-dev \
  && pecl install imagick && docker-php-ext-enable imagick \
  && rm -rf /var/lib/apt/lists/*

# Install dependencies for WordPress
RUN docker-php-ext-install mysqli opcache pdo_mysql zip exif

# Install GD
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j "$(nproc)" gd

RUN a2enmod rewrite

RUN cat /etc/modsecurity/modsecurity.conf-recommended \
    | sed 's#^SecRuleEngine .*#SecRuleEngine On#g' \
    | sed 's#^SecAuditLog .*#SecAuditLog /dev/stdout#g' \
    | sed 's#^SecDataDir .*#SecDataDir /run/apache2/modsecurity/data#g' \
    | sed 's#^SecTmpDir .*#SecTmpDir /run/apache2/modsecurity/tmp#g' \
    | sed 's#^SecAuditEngine .*#SecAuditEngine Off#g' \
    > /etc/modsecurity/modsecurity.conf
RUN mkdir /etc/modsecurity/rules.pre
RUN mkdir /etc/modsecurity/rules.post

RUN echo "ServerTokens Prod\n" >> /etc/apache2/apache2.conf
RUN echo "ServerSignature Off\n" >> /etc/apache2/apache2.conf
