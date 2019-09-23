# Docker MariaDB

## Info
- **Contenedor nombre**: mariadb
- **Puero**: 3306
- **Usuario**: root
- **Contraseña**: 1234

## Permisos remotos
~~~~
docker exec -it mariadb mysql -u root -p
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '1234' WITH GRANT OPTION;
~~~~

## File
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
      MYSQL_ROOT_PASSWORD: 1234
    volumes:
      - ./datos:/var/lib/mysql
    command: ['mysqld', '--character-set-server=utf8mb4', '--collation-server=utf8mb4_unicode_ci']
~~~
