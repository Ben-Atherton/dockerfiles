FROM php:8.0.6-apache
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Packages
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  wget \
  # needed for Linode CLI
  python3-pip \
  python3-setuptools \
  # needed for zip
  zip \
  libzip-dev \
  unzip \
  && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install DOCTL
RUN wget https://github.com/digitalocean/doctl/releases/download/v1.60.0/doctl-1.60.0-linux-amd64.tar.gz \
  && tar xf doctl-1.60.0-linux-amd64.tar.gz \
  && mv doctl /usr/local/bin

# Install Linode CLI
RUN pip3 install linode-cli

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
  && unzip awscliv2.zip \
  && ./aws/install