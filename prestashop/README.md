# Docker Prestashop

## Info
- **Contenedor nombre**: prestashop
- **Puerto**: 8080
- **Imagen**: prestashop/prestashop:latest
- **Base de datos**: MariaDB

## Info MariaDB
Obtener el nombre del HOST del contenedor de MariaDB para la configuracion de Prestashop en la conexion a la base de datos
~~~
docker inspect mariadb | grep Hostname
~~~
Resultado:
~~~
"HostnamePath": "/var/snap/docker/common/var-lib-docker/containers/db09806e787b87f831be68044ef02a9027d42d345e30fe681f123a740ac81856/hostname",
            "Hostname": "db09806e787b",
~~~

## Post Install
- Eliminar la carpeta "INSTALL"
~~~
docker exec -it prestashop rm -R install
~~~
- Cambiar nombre de la carpeta "ADMIN" a "PANEL". El nuevo nombre es como se desee 
~~~
docker exec -it prestashop mv admin panel
~~~

## Usando docker-compose
~~~
version: '3.1'
services:
  prestashop:
    container_name: prestashop
    restart: always
    image: prestashop/prestashop:latest
    ports:
      - "8080:80"
    environment:
      PS_INSTALL_AUTO: 0
      PS_DEV_MODE: 0
      PS_DEMO_MODE: 0
      PS_LANGUAGE: es-mx
      PS_COUNTRY: co
    networks:
      - default
      - mariadb_default
networks:
  default:
    driver: bridge
  mariadb_default:
    external: true
~~~
~~~
docker-compose d -up
~~~
# Alternativa
~~~
version: '3.3'
services:
  cafe:
    restart: always 
    build:
      context: .
      dockerfile: ./Dockerfile
    container_name: cafe
    environment:
      XDEBUG_CONFIG: remote_host=172.17.0.1 remote_port=9000 remote_enable=1
    ports:
      - '15000:80'
    volumes:
      - './web:/var/www/html'
    networks:
      - default
      - mariadb_default
networks:
  mariadb_default:
    external:
      name: mariadb_default
~~~
~~~
FROM php:apache

RUN pecl install -f xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini;

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    zip \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo pdo_mysql libzip

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && sync && \
    install-php-extensions gd xdebug

RUN a2enmod rewrite
~~~
