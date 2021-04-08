FROM owasp/modsecurity:latest

RUN set -ex; \
    mkdir /etc/nginx/modsec; \ 
    wget https://github.com/SpiderLabs/owasp-modsecurity-crs/archive/v3.0.2.tar.gz; \
    tar -xzf v3.0.2.tar.gz -C /etc/nginx/modsec; \
    cp /etc/nginx/modsec/owasp-modsecurity-crs-3.0.2/crs-setup.conf.example /etc/nginx/modsec/owasp-modsecurity-crs-3.0.2/crs-setup.conf