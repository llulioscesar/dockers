~~~
version: '3.3'
services:
  phpmyadmin:
    restart: always 
    image: phpmyadmin
    container_name: phpmyadmin
    environment:
      PMA_HOST: mariadb
      PMA_PORT: 3306
      PMA_USER: root
      PMA_PASSWORD: 1234
    ports:
      - '15001:80'
    networks:
      - default
      - mariadb_default
networks:
  mariadb_default:
    external:
      name: mariadb_default
~~~
