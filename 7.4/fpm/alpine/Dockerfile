FROM php:7.4-fpm-alpine

ENV CFLAGS="-I/usr/src/php"

RUN apk --update --no-cache add shadow libpng-dev jpeg-dev libxml2-dev libxslt-dev libzip-dev freetype-dev \
  postgresql-dev libxml2-dev zlib-dev icu-dev gettext-dev oniguruma-dev

COPY php.ini-development /usr/local/etc/php/php.ini

RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-configure intl --enable-intl

RUN docker-php-ext-install dom gd intl json gettext mbstring mysqli pdo pdo_mysql pdo_pgsql pgsql \
  phar posix simplexml soap xml xmlreader xmlrpc xmlwriter xsl zip

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

RUN find / -group 82 -exec chgrp -h www-data {} \; && find / -user 82 -exec chown -h www-data {} \;

EXPOSE 9000

CMD ["php-fpm"]
