# Docker - PHP

![Docker Pulls](https://img.shields.io/docker/pulls/weef/php.svg)
![Docker Automated](https://img.shields.io/docker/automated/weef/php.svg)
![Docker Build](https://img.shields.io/docker/build/weef/php.svg)

Esse repositorio armazena o codigo-fonte do arquivo de construcao das imagens do PHP e PHP para o Laravel, para uso
com o Docker.

* [Caracteristicas](#caracteristicas)
  * [PHP](#imagem-base)
  * [Laravel](#laravel)
* [Dockerfiles](#tags-e-dockerfiles)
* [Construindo as imagens](#construindo-as-imagens)
* [Usando as imagens (sem orquestracao)](#usando-as-imagens)

## Caracteristicas

### Imagem base

A imagem base conta com:

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
  
### Laravel

A imagem conta com:

* As pastas de cache e configuracao criadas;
* [Laravel](https://laravel.com/docs/) instalado de forma global com o Composer;

## Tags e Dockerfiles

* 7.3
  * [7.3-fpm](7.3/fpm/Dockerfile)
  * [7.3-fpm-laravel](7.3/fpm/Dockerfile.Laravel)
  
## Construindo as imagens

Para construir as imagens localmente para testes ou adicao de novas dependencias:

Imagem PHP-FPM

```bash
docker build -t weef/php:7.3-fpm 7.3/fpm
```

Imagem PHP-FPM-Laravel

```bash
docker build -t weef/php:7.3-fpm -f 7.3/fpm/Dockerfile.Laravel 7.3/fpm
```

## Usando as imagens

Para executar utilizar a imagem:

Exemplos:

```bash
docker run -it -v fake_webroot_directory:/var/www/html weef/php:7.3-fpm bash
```

```bash
docker run -it weef/php:7.3-fpm php -v
```



  
