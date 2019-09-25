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
