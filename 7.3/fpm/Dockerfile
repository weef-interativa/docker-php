FROM php:7.3-fpm

ARG DEFAULT_USER_ID=1000
ARG DEFAULT_GROUP_ID=1000
ARG PHPDOC_PHAR_URL="https://github.com/phpDocumentor/phpDocumentor2/releases/download/v2.9.0/phpDocumentor.phar"

RUN apt-get update -y && apt-get install -y sudo unzip libmcrypt-dev libzip-dev wget git gcc make autoconf \
    pkg-config libmagickwand-dev libevent-dev libssl-dev libfreetype6-dev libwebp-dev libpq-dev libsnmp-dev \
    libxml2-dev libjpeg62-turbo-dev libpng-dev libgmp-dev mariadb-client --no-install-recommends

RUN pecl channel-update pecl.php.net

RUN curl -o /usr/local/bin/phpdoc -L "$PHPDOC_PHAR_URL"&& chmod +x /usr/local/bin/phpdoc

RUN docker-php-ext-install bcmath bz2 dom gd gettext hash intl json mbstring mysqli pdo pdo_mysql pdo_pgsql pgsql phar \
    posix simplexml soap xml xmlrpc xmlwriter zip

RUN export CFLAGS="-I/usr/src/php" && docker-php-ext-configure xmlreader && docker-php-ext-install xmlreader

RUN pecl install imagick mcrypt-1.0.2 && docker-php-ext-enable imagick mcrypt

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

USER www-data