# Docker Magento2

1. Cree una nueva red para la aplicación:
~~~
docker network create magento-tier
~~~
2. Cree un volumen para la persistencia MariaDB
~~~
docker volume create --name mariadb_data
~~~
