FROM httpd:2.4.46-alpine
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Packages
RUN apk update; \
    apk upgrade;

# Copy apache vhost file to proxy php requests to php-fpm container
ADD https://raw.githubusercontent.com/Ben-Atherton/dockerfiles/master/apache/defaulthost.apache.conf /usr/local/apache2/conf/defaulthost.apache.conf
RUN echo "Include /usr/local/apache2/conf/defaulthost.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf

RUN echo "ServerSignature Off\n" >> /usr/local/apache2/conf/httpd.conf
