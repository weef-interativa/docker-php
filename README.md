# Docker - PHP

![Docker Pulls](https://img.shields.io/docker/pulls/weef/php.svg)
![Docker Automated](https://img.shields.io/docker/cloud/automated/weef/php.svg)
![Docker Build](https://img.shields.io/docker/cloud/build/weef/php.svg)

Esse repositorio armazena o codigo-fonte do arquivo de construcao das imagens do PHP-FPM, PHP-FPM para o Laravel, e 
PHP-FPM com base no Linux Alpine, para uso com o Docker.

* [Caracteristicas](#caracteristicas)
  * [PHP](#imagem-base)
  * [Laravel](#laravel)
* [Dockerfiles](#tags-e-dockerfiles)

## Caracteristicas

### Imagem base

A imagem base conta com:

* O ID/GID do usuario www-data foi definido como 1000:1000;
* O arquivo php.ini esta configurado para ambientes de desenvolvimento;
* [Composer](http://getcomposer.org/http://getcomposer.org/) globalmente instalado;
* Os seguintes pacotes de sistema:
  * Debian:
    * sudo
    * unzip 
    * wget
    * git
    * gcc
    * make
    * autoconf
    * pkg-config 
    * mariadb-client
  * Alpine:
    * shadow 
    * libpng-dev
    * jpeg-dev
    * libxml2-dev
    * libxslt-dev
    * libzip-dev
    * freetype-dev
    * postgresql-dev 
    * libxml2-dev
    * zlib-dev
    * icu-dev
    * gettext-dev
    
* Os seguintes pacotes PHP:
  * bcmath (Somente Debian)
  * bz2 (Somente Debian)
  * dom
  * gd (com suporte a PNG, JPG e TrueType)
  * gettext
  * hash
  * intl
  * json
  * mbstring
  * mysqli
  * pdo 
  * pdo_mysql
  * pdo_pgsql 
  * pgsql 
  * phar
  * posix 
  * simplexml 
  * soap 
  * xml 
  * xmlrpc
  * xmlwriter 
  * zip
  * xmlreader
  * imagick
  * mcrypt
  
### Laravel

A imagem conta com:

* As pastas de cache e configuracao criadas;
* [Laravel](https://laravel.com/docs/) instalado de forma global com o Composer;

## Tags e Dockerfiles

* 7.1
  * [7.1-fpm](7.1/fpm/debian/Dockerfile)
  * [7.1-fpm-laravel](7.1/fpm/debian/Dockerfile#L35)
* 7.3
  * [7.3-fpm](7.3/fpm/debian/Dockerfile)
  * [7.3-fpm-laravel](7.3/fpm/debian/Dockerfile#L34)
  * [7.3-fpm-alpine3.9](7.3/fpm/alpine/3.9/Dockerfile)
* 7.4
  * [7.4-fpm](7.4/fpm/debian/Dockerfile)
  * [7.4-fpm-laravel](7.4/fpm/debian/Dockerfile#L34)
  * [7.4-fpm-alpine3.9](7.4/fpm/alpine/3.9/Dockerfile)



  
