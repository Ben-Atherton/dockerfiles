FROM debian:buster
LABEL maintainer "Ben Atherton <ben@benatherton.com>"

# Packages
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  apache2 \
  # needed for ModSecurity & OWASP ModSecurity CRS
  libapache2-mod-security2 \
  modsecurity-crs \
  && rm -rf /var/lib/apt/lists/*

ADD https://raw.githubusercontent.com/Ben-Atherton/dockerfiles/master/apache/security2.conf /etc/apache2/mods-available/security2.conf

# Copy apache vhost file to proxy php requests to php-fpm container
ADD https://raw.githubusercontent.com/Ben-Atherton/dockerfiles/master/apache/defaulthost.apache.conf /usr/local/apache2/conf/defaulthost.apache.conf
RUN echo "Include /usr/local/apache2/conf/defaulthost.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf

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
