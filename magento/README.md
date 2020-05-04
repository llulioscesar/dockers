# Docker Magento2

1. Cree una nueva red para la aplicación:
~~~
docker network create magento-tier
~~~
2. Cree un volumen para la persistencia MariaDB
~~~
docker volume create --name mariadb_data
~~~

## docker-compose
~~~
version: '3.1'
services:
  magento2:
    image: 'bitnami/magento:2'
    environment:
      - MARIADB_HOST=mariadb
      - MARIADB_PORT_NUMBER=3306
      - MAGENTO_DATABASE_USER=root
      - MAGENTO_DATABASE_PASSWORD=1234
      - MAGENTO_DATABASE_NAME=magento2
      - ELASTICSEARCH_HOST=elasticsearch
      - ELASTICSEARCH_PORT_NUMBER=9200
    ports:
      - '80:80'
      - '443:443'
    volumes:
      - './datos:/bitnami'
    depends_on:
      - mariadb
      - elasticsearch
  elasticsearch:
    image: 'bitnami/elasticsearch:6'
    volumes:
      - './elasticsearch_data:/bitnami/elasticsearch/data'
volumes:
  elasticsearch_data:
    driver: local
  mariadb_data:
    driver: local
  magento_data:
    driver: local  
~~~
