FROM owasp/modsecurity:nginx

RUN set -ex; \
    mkdir /etc/nginx/modsec; \
    wget https://github.com/coreruleset/coreruleset/archive/v3.3.0.tar.gz; \
    tar -xzf v3.3.0.tar.gz -C /etc/nginx/modsec