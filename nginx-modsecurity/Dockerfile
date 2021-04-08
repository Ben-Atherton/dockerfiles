FROM owasp/modsecurity:latest

RUN set -ex; \
    mkdir /etc/nginx/modsec; \ 
    wget https://github.com/coreruleset/coreruleset/archive/v3.3.0.tar.gz; \
    tar -xzf v3.3.0.tar.gz -C /etc/nginx/modsec; \
    cp /etc/nginx/modsec/coreruleset-3.3.0/crs-setup.conf.example /etc/nginx/modsec/coreruleset-3.3.0/crs-setup.conf