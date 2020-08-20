FROM php:7.4-fpm

ARG DEFAULT_USER_ID=1000
ARG DEFAULT_GROUP_ID=1000
ARG PHPDOC_PHAR_URL="https://github.com/phpDocumentor/phpDocumentor/releases/download/v2.9.1/phpDocumentor.phar"

RUN apt-get update -y && pecl channel-update pecl.php.net && apt-get install -y sudo unzip wget git gcc make \
 autoconf pkg-config mariadb-client libmcrypt-dev libzip-dev libmagickwand-dev libevent-dev libssl-dev \
 libfreetype6-dev libwebp-dev libjpeg-dev libpq-dev libsnmp-dev libxml2-dev libjpeg62-turbo-dev libpng-dev \
 libgmp-dev libonig-dev --no-install-recommends

COPY php.ini-development /usr/local/etc/php/php.ini

RUN curl -o /usr/local/bin/phpdoc -L "$PHPDOC_PHAR_URL" && chmod +x /usr/local/bin/phpdoc

RUN docker-php-ext-configure gd --with-freetype --with-jpeg

RUN export CFLAGS="-I/usr/src/php" && docker-php-ext-configure xmlreader && docker-php-ext-install xmlreader

RUN docker-php-ext-install bcmath bz2 dom gd gettext intl json mbstring mysqli pdo pdo_mysql pdo_pgsql pgsql phar \
    posix simplexml soap xml xmlrpc xmlwriter zip && docker-php-source delete

RUN EXPECTED_SIGNATURE="$(wget -q -O - https://composer.github.io/installer.sig)"
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN ACTUAL_SIGNATURE="$(php -r "echo hash_file('sha384', 'composer-setup.php');")"

RUN if [ "$EXPECTED_SIGNATURE" != "$ACTUAL_SIGNATURE" ]; then echo 'ERROR: Invalid installer signature' && rm composer-setup.php && exit 1; fi

RUN php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN chown -R $DEFAULT_USER_ID:$DEFAULT_GROUP_ID /var/www/html

RUN usermod -aG sudo www-data && \
    usermod -aG root www-data && \
    usermod -u $DEFAULT_USER_ID www-data && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

VOLUME /usr/local/etc/php

USER www-data