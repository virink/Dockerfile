FROM php:5.4-fpm-alpine

LABEL Author="Virink <virink@outlook.com>"
LABEL Blog="https://www.virzz.com"
LABEL GitRepo="https://github.com/virink/Dockerfiles"

COPY files /tmp/

RUN docker-php-source extract \
    && cd /usr/src/php/ext \
    && wget -O xdebug.tgz https://xdebug.org/files/xdebug-2.4.1.tgz \
    && mkdir xdebug \
    && tar -xzf xdebug.tgz -C /usr/src/php/ext/xdebug --strip-components=1 \
    && docker-php-ext-install xdebug \
    && docker-php-source delete \
    && mv /tmp/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini \
    && mv /tmp/docker-php-entrypoint /usr/local/bin/docker-php-entrypoint \
    && mkdir /run/nginx \
    && apk add --update --no-cache nginx \
    && mv /tmp/nginx.conf /etc/nginx/nginx.conf \
    && mv /tmp/vhost.nginx.conf /etc/nginx/conf.d/default.conf\
    && ln -s /var/www/html /www

EXPOSE 80

VOLUME ["/www","/var/log/nginx"]

CMD ['/bin/sh', '-c', 'docker-php-entrypoint']