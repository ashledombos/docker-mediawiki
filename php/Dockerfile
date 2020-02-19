FROM alpine:3
RUN apk --no-cache add \
        php7 \
        php7-apcu \
        php7-intl \
        php7-mbstring \
        php7-xml \
        php7-mysqlnd \
        php7-fileinfo \
        php7-json \
        php7-session \
        php7-curl \
        php7-pecl-imagick \
        php7-ldap \
        imagemagick \
        mini-sendmail \
        diffutils

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
    echo 'opcache.memory_consumption=128'; \
    echo 'opcache.interned_strings_buffer=8'; \
    echo 'opcache.max_accelerated_files=4000'; \
    echo 'opcache.revalidate_freq=2'; \
    echo 'opcache.fast_shutdown=1'; \
    echo 'opcache.enable_cli=0'; \
    } > /etc/php7/conf.d/opcache-recommended.ini

# PHP
ENV PHP_MAX_EXECUTION_TIME 60
ENV PHP_MEMORY_LIMIT 256M
ENV PHP_POST_MAX_SIZE 40M
ENV PHP_UPLOAD_MAX_FILESIZE 32M
ENV PHP_TIMEZONE America/Guadeloupe

EXPOSE 9000

RUN set -x \
    && addgroup -g 1000 -S apache \
    && adduser -u 1000 -D -S -G apache apache

COPY ./docker-entrypoint.sh /

ENTRYPOINT ["sh","/docker-entrypoint.sh"]

CMD ["php-fpm"]

