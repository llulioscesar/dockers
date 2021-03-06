# Docker MariaDB

## Info
- **Contenedor nombre**: mariadb
- **Puero**: 3306
- **Usuario**: root
- **Contraseña**: 1234
- **Imagen**: mariadb:latest

## Permisos remotos
~~~~
docker exec -it mariadb mysql -u root -p
~~~~
~~~~
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '1234' WITH GRANT OPTION;
~~~~

## Cree un volumen para la persistencia MariaDB
~~~
docker volume create --name mariadb_data
~~~

## docker-compose (Unix)
~~~
version: '3.1'
services:
  mariadb:
    container_name: mariadb
    restart: always
    image: mariadb:latest
    ports:
      - "3306:3306"
    environment:
      ALLOW_EMPTY_PASSWORD: "yes"
      MYSQL_ROOT_PASSWORD: 1234
    volumes:
      - ./datos:/var/lib/mysql
    command: ['mysqld', '--character-set-server=utf8mb4', '--collation-server=utf8mb4_unicode_ci']
~~~

## docker-compose (Windows)
~~~
version: '3.1'
services:
  mariadb:
    container_name: mariadb
    restart: always
    image: mariadb:latest
    ports:
      - "3306:3306"
    environment:
      ALLOW_EMPTY_PASSWORD: "yes"
      MYSQL_ROOT_PASSWORD: 1234
    volumes:
      - mariadb_data
    command: ['mysqld', '--character-set-server=utf8mb4', '--collation-server=utf8mb4_unicode_ci']
  mariadb_data:
    image: busybox
    volumes:
      - ./datos:/var/lib/mysql
~~~
~~~
docker-compose up -d
~~~
