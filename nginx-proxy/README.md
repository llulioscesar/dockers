# Nginx Proxy

## Info
- **Puerto**: 80
- **Contenerdor nombre**: nginx-proxy
- **[Mas informacion](https://github.com/jwilder/nginx-proxy)**

## Crear red
Ejecutar antes de crear el contenedor
~~~
docker network create nginx-proxy
~~~

## En linea
~~~
docker run -d -p 80:80 --name nginx-proxy --net nginx-proxy -v /var/run/docker.sock:/tmp/docker.sock jwilder/nginx-proxy
~~~

## docker-compose.yml
~~~
version: "3.1"
services:
  nginx-proxy:
    image: jwilder/nginx-proxy
    container_name: nginx-proxy
    ports:
      - "80:80"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro

networks:
  default:
    external:
      name: nginx-proxy
~~~
~~~
docker-compose up -d
~~~
