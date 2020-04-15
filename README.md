# Docker - PHP

Esse repositorio armazena o codigo-fonte do arquivo de construcao das imagens do PHP e PHP para o Laravel, para uso
com o Docker.

# Caracteristicas

## PHP

As imagens contam com:

* O ID/GID do usuario www-data foi definido como 1000:1000;
* O arquivo php.ini esta configurado para ambientes de desenvolvimento;
* [Composer](http://getcomposer.org/http://getcomposer.org/) globalmente instalado;
* [phpDocumentor 2.9.0 (phar)](https://www.phpdoc.org/) globalmente instalado;
* Os seguintes pacotes de sistema:
  * sudo
  * unzip 
  * wget
  * git
  * gcc
  * make
  * autoconf
  * pkg-config 
  * mariadb-client
* Os seguintes pacotes PHP:
  * bcmath
  * bz2
  * dom
  * gd
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
  
## Laravel

A imagem conta com:

* As pastas de cache e configuracao criadas;
* [Laravel](https://laravel.com/docs/) instalado de forma global com o Composer;

# Tags e respectivos Dockerfile

* 7.3
  * [7.3-fpm](7.3/fpm/Dockerfile)
  * [7.3-fpm-laravel](7.3/fpm/Dockerfile.Laravel)
  
