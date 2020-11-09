FROM php:7.3-fpm AS BASE

ARG DEFAULT_USER_ID=1000
ARG DEFAULT_GROUP_ID=1000

RUN apt-get update -y && pecl channel-update pecl.php.net && apt-get install -y unzip wget git gcc make autoconf \
    pkg-config mariadb-client libmcrypt-dev libzip-dev libmagickwand-dev libevent-dev libssl-dev libfreetype6-dev \
    libwebp-dev libjpeg-dev libpq-dev libsnmp-dev libxml2-dev libjpeg62-turbo-dev libpng-dev libgmp-dev --no-install-recommends

COPY php.ini-development /usr/local/etc/php/php.ini

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN export CFLAGS="-I/usr/src/php" && docker-php-ext-configure xmlreader && docker-php-ext-install xmlreader

RUN docker-php-ext-install bcmath bz2 dom gd gettext hash intl json mbstring mysqli pdo pdo_mysql pdo_pgsql pgsql phar \
    posix simplexml soap xml xmlrpc xmlwriter zip

RUN pecl install imagick mcrypt-1.0.2 && docker-php-ext-enable imagick mcrypt

RUN EXPECTED_SIGNATURE="$(wget -q -O - https://composer.github.io/installer.sig)"
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN ACTUAL_SIGNATURE="$(php -r "echo hash_file('sha384', 'composer-setup.php');")"

RUN if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]; then echo 'ERROR: Invalid installer signature' && rm composer-setup.php && exit 1; fi

RUN php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN chown -R $DEFAULT_USER_ID:$DEFAULT_GROUP_ID /var/www/html

VOLUME /usr/local/etc/php

FROM BASE as LARAVEL

RUN mkdir -p /var/www/.config /var/www/.composer && \
  chown -R www-data:www-data /var/www/.config /var/www/.composer

VOLUME /var/www/html

RUN composer global require laravel/installer
