FROM alpine:latest
COPY mediawiki.apache.conf /etc/apache2/conf.d/mediawiki.apache.conf

RUN set -x \
    && addgroup -g 1000 -S apache \
    && adduser -u 1000 -D -S -G apache apache

RUN apk add --no-cache \
    apache2-proxy \
    apache2-utils \
    logrotate 

RUN sed -i '/LoadModule mpm_prefork_module/s/^/#/g' /etc/apache2/httpd.conf \
    && sed -i '/LoadModule mpm_event_module/s/^#//g' /etc/apache2/httpd.conf


WORKDIR /var/www/html/

EXPOSE 80

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
